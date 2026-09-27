# 🤝 TEAM HANDOVER GUIDE — Resto (Restaurant Platform)

**Read this fully before writing any code.** This document explains *everything* that has been
done so far: how the backend was created file-by-file, how the frontend was created and what
was changed in it (before → after), how the two talk to each other, and — most importantly —
**how the two of us will work together without breaking anything** (Git, shared MongoDB, shared Postman).

> 👤 Written for: Developer #2 joining the project
> 📅 Project state: Backend skeleton working, Flutter ↔ Node connection proven, MongoDB NOT yet connected
> 🚫 Rule for this doc: it only *explains* — no code was changed to write it

---

# TABLE OF CONTENTS

1. [What the project is + big picture](#1-what-the-project-is--big-picture)
2. [Repository folder map](#2-repository-folder-map)
3. [PART A — How the BACKEND was created (full story)](#3-part-a--how-the-backend-was-created-full-story)
4. [PART B — How the FRONTEND was created + every change (before → after)](#4-part-b--how-the-frontend-was-created--every-change-before--after)
5. [PART C — How frontend connects to backend (the bridge)](#5-part-c--how-frontend-connects-to-backend-the-bridge)
6. [PART D — How WE will share the work (Git rules for 2 devs)](#6-part-d--how-we-will-share-the-work-git-rules-for-2-devs)
7. [PART E — Two developers, ONE MongoDB database](#7-part-e--two-developers-one-mongodb-database)
8. [PART F — ONE Postman for testing endpoints together](#8-part-f--one-postman-for-testing-endpoints-together)
9. [PART G — Who works on which files (ownership map)](#9-part-g--who-works-on-which-files-ownership-map)
10. [Known quirks / typos to fix later (do NOT panic seeing them)](#10-known-quirks--typos-to-fix-later)
11. [Quick command cheat sheet](#11-quick-command-cheat-sheet)
12. [Mental model — remember only these 5 lines](#12-mental-model--remember-only-these-5-lines)

---

# 1. What the project is + big picture

We are building a **Swiggy / Zomato style restaurant platform**.

| Piece | Technology | What it does |
|---|---|---|
| Customer app (frontend) | **Flutter** (Dart) | UI: home, search, restaurant details, cart, dineout, profile |
| Backend API | **Node.js + Express** | The "brain": routes, business logic, security |
| Database | **MongoDB** (via Mongoose) | Stores users, restaurants, menu, orders (⚠️ connection not built yet) |
| Legacy backend (being replaced) | **Supabase** | The Flutter app currently still reads data from Supabase — we are migrating everything to Node + MongoDB |

### The one diagram to remember

```
┌────────────────────┐      HTTP + JSON        ┌────────────────────┐      Mongoose      ┌──────────┐
│   FLUTTER APP      │ ──────────────────────► │   NODE.JS BACKEND  │ ─────────────────► │ MONGODB  │
│  (screens / UI)    │ ◄────────────────────── │  Express  :5000    │ ◄───────────────── │          │
└────────────────────┘   /api/v1/...           └────────────────────┘                    └──────────┘
```

**Golden rule:** Flutter NEVER talks to MongoDB directly. Flutter only calls HTTP endpoints
like `GET http://localhost:5000/api/v1/health`. Only Node talks to MongoDB.

---

# 2. Repository folder map

```
resto/  (the Git repo root, branch: main)
│
├── backend/                  ← Node.js + Express API   (NEW — not yet committed to Git!)
│   ├── package.json          ← project config + dependency list
│   ├── package-lock.json     ← exact dependency versions
│   ├── .env                  ← LOCAL SECRETS (never commit, never share in chat)
│   ├── .env.example          ← safe template showing which variables are needed
│   ├── .gitignore            ← ⚠️ currently EMPTY — see section 6 "critical warning"
│   ├── README.md
│   ├── docs/
│   │   ├── 01-project-setup.md
│   │   └── 02-express-architecture.md
│   └── src/
│       ├── server.js         ← starts the HTTP server (entry point)
│       ├── app.js            ← creates & configures Express app
│       ├── config/
│       │   ├── env.js        ← reads .env into one JS object
│       │   └── database.js   ← ⚠️ EMPTY — MongoDB connection goes here (Phase 3)
│       ├── middleware/
│       │   ├── notFound.middleware.js  ← 404 handler
│       │   └── error.middleware.js     ← global error handler
│       ├── routes/
│       │   ├── index.js      ← central route registration (/api/v1)
│       │   └── health.routes.js  ← the health-check API
│       ├── modules/          ← 20 EMPTY feature folders prepared (auth, menu, orders, …)
│       ├── sockets/          ← empty (Socket.IO comes later)
│       └── utils/            ← empty (helpers come later)
│
├── frontend/                 ← Flutter customer app
│   ├── pubspec.yaml          ← Flutter dependency list (2 changes made — see Part B)
│   └── lib/
│       ├── main.dart                     ← normal app entry (Supabase init + app)
│       ├── main_backend_check.dart       ← NEW: alternate entry to test Node connection
│       ├── app/
│       │   ├── app.dart                  ← MaterialApp shell + main page with navbar
│       │   └── theme/                    ← app colors + text styles
│       ├── core/
│       │   ├── config/
│       │   │   ├── api_config.dart       ← NEW: backend URL lives here
│       │   │   └── supabase_config.dart  ← legacy Supabase URL + key
│       │   ├── network/
│       │   │   └── api_client.dart       ← NEW: HTTP helper for calling Node
│       │   └── widgets/                  ← navbar.dart, bottomnav.dart
│       ├── data/
│       │   ├── models/restaurant_model.dart
│       │   └── repositories/
│       │       ├── restaurant_repository.dart        ← STILL Supabase (legacy)
│       │       └── backend_health_repository.dart    ← NEW: calls Node /health
│       └── features/                     ← all screens
│           ├── splash/  home/  search/  dineout/  cart/  draft/  profile/  restaurant/
│           └── connection/
│               └── backend_connection_page.dart      ← NEW: visual "Connected ✓" test screen
│
└── Docs/
    ├── idea.md, app.md               ← original product idea notes
    ├── COMPLETE-PROJECT-GUIDE.md     ← earlier guide (run instructions focus)
    └── HANDOVER-GUIDE-FOR-TEAM.md    ← THIS FILE
```

---

# 3. PART A — How the BACKEND was created (full story)

Told exactly in the order it was done, so you can reproduce it from zero if needed.

## Step A1 — Create the Node project

```bash
cd backend
npm init -y
```

This created `package.json`. We then edited it so the scripts point at our entry file:

```json
{
  "name": "backend",
  "version": "1.0.0",
  "main": "src/server.js",
  "scripts": {
    "start": "node src/server.js",
    "dev": "nodemon src/server.js"
  }
}
```

* `npm run dev` → development command (auto-restarts on file save)
* `npm start` → plain start (for production later)

## Step A2 — Install the packages (exact commands used)

```bash
npm install express mongoose cors dotenv helmet
npm install --save-dev nodemon
```

| Package | Version installed | Why we need it |
|---|---|---|
| `express` | ^5.2.1 | Creates the HTTP API server + routing |
| `mongoose` | ^9.10.2 | Talks to MongoDB using schemas/models (installed now, used in Phase 3) |
| `cors` | ^2.8.6 | Allows Flutter/Chrome (different origin) to call our API |
| `dotenv` | ^18.0.4 | Loads secrets from `.env` into `process.env` |
| `helmet` | ^8.3.0 | Adds security HTTP headers automatically |
| `nodemon` (dev) | ^3.1.14 | Auto-restarts server when code changes — dev convenience only |

## Step A3 — Create the folder structure

```
src/
├── config/       ← env vars, database connection
├── middleware/    ← express middlewares (errors, 404)
├── modules/       ← business features (auth, menu, orders…) — one folder per feature
├── routes/        ← central route registration
├── sockets/       ← realtime (Socket.IO, later)
├── utils/         ← shared helpers (later)
├── app.js         ← configure Express
└── server.js      ← start the server
```

**Why modules/ has 20 empty folders?** We pre-planned the features so both of us know where
code will live: `auth, users, restaurants, branches, staff, menu, tables, bookings, cart,
orders, kot, billing, coupons, reviews, payments, delivery, notifications, analytics,
support, ai`. Each module will follow the same internal pattern: `module.routes.js`,
`module.controller.js`, `module.service.js`, `module.model.js`.

## Step A4 — The files, one by one (actual current code)

### 3.1 `src/config/env.js` — the environment loader

```js
const dotenv = require("dotenv");

dotenv.config();

const env = {
  port: process.env.PORT || 5000,
  nodeEnv: process.env.NODE_ENV || "development",
};

module.exports = env;
```

**What it does:** reads `backend/.env` once and exposes values as `env.port`, `env.nodeEnv`.
Everywhere else in the app we use `env.port` instead of repeating `process.env.PORT`.
Fallbacks (`|| 5000`) keep the server running even if a variable is missing.

### 3.2 `backend/.env` vs `backend/.env.example`

`.env` (private — real values, lives only on your machine):

```env
PORT=5000
NODE_ENV=development
```

`.env.example` (safe — committed to Git, shows the teammate WHICH variables are needed):

```env
PORT=5000
NODE_ENV=development
```

> ⚠️ Later when we add MongoDB, we add `MONGODB_URI=...` to BOTH files — real URI only in `.env`,
> placeholder in `.env.example`. See Part E.

### 3.3 `src/app.js` — the Express application (the heart)

```js
const express = require("express");
const cors = require("cors");
const helmet = require("helmet");

const routes=require("./routes")
const notFound=require("./middleware/notFound.middleware");
const errorHandler=require("./middleware/error.middleware")


const app = express();

// Security middleware
app.use(helmet());

// Enable CORS
app.use(cors());

// Parse JSON request bodies
app.use(express.json());

// API Routes
app.use("/api/v1",routes)


// handle unknown routes
app.use(notFound)

// Globale error Handler
app.use(errorHandler)

module.exports = app;
```

**Line-by-line meaning:**

| Line | Purpose |
|---|---|
| `helmet()` | Adds safe HTTP headers (basic protection) |
| `cors()` | Lets browsers/Flutter-web call us from another origin without CORS errors |
| `express.json()` | Converts incoming JSON body → `req.body` object |
| `app.use("/api/v1", routes)` | Every route in `routes/index.js` gets the prefix `/api/v1` — **API versioning** |
| `app.use(notFound)` | Anything that didn't match a route falls through to the 404 handler |
| `app.use(errorHandler)` | Any thrown error lands here — must be LAST, after routes |

**Middleware order matters!** helmet → cors → json → routes → 404 → error. If the error
handler were before the routes, it would never catch their errors.

### 3.4 `src/server.js` — the starter

```js
const app = require("./app");
const env = require("./config/env");

app.listen(env.port, () => {
  console.log(`Server running on port ${env.port}`);
});
```

**Why split app.js and server.js?** `app.js` is the *configurable* Express app (can be tested
without opening a port); `server.js` is the tiny *launcher*. This separation makes testing
and future deployment cleaner.

### 3.5 `src/routes/index.js` — central router

```js
const express = require("express");

const healthRoutes = require("./health.routes");

const router = express.Router();

router.use(healthRoutes);

module.exports = router;
```

When we add modules later, they get attached here, e.g.:

```js
router.use("/auth", authRoutes);
router.use("/restaurants", restaurantRoutes);
```

Full URL = `/api/v1` (from app.js) + `/auth` (from here) + `/login` (from module) etc.

### 3.6 `src/routes/health.routes.js` — first working API

```js
const express = require("express");

const router = express.Router();

router.get("/health", (req, res) => {
  res.status(200).json({
    success: true,
    message: "Restaurant backend is running",
  });
});

module.exports = router;
```

### 3.7 `src/middleware/notFound.middleware.js` — 404 handler

```js
const notFound=(req,res)=>{
    res.status(404).json({
        success:false,
        message:`Route not Found: ${req.originalURL}`
    });
};

module.exports=notFound
```

### 3.8 `src/middleware/error.middleware.js` — global error handler

```js
const errorHandler=(err,req,res,next)=>{
    console.error(err)

    const stausCode=err.stausCode || 500;

    res.status(stausCode).json({
        success:false,
        message:err.message || "Internal Server Error"
    });
};

module.exports=errorHandler;
```

> ⚠️ Yes, `stausCode` is misspelled (should be `statusCode`) — see section 10. It still works
> because it's consistent within the file. Don't "fix" it silently — we'll fix it together.

## Step A5 — The complete request flow

```
Flutter / Chrome / Postman
        │  HTTP request
        ▼
http://localhost:5000/api/v1/...
        ▼
server.js (listening)
        ▼
app.js middlewares in order:
   helmet → cors → express.json
        ▼
routes/index.js  (matches /api/v1/*)
        ▼
specific route (health.routes.js today, module routes tomorrow)
        ▼
response JSON sent back
        ▼
no route matched?  → notFound.middleware  → 404 JSON
error thrown?      → error.middleware      → error JSON
```

## Step A6 — Run it and prove it works

```bash
cd backend
npm install        # only needed once / after pulling new packages
npm run dev
```

Expected console output:

```
Server running on port 5000
```

Test (browser, Postman, or PowerShell):

```
GET http://localhost:5000/api/v1/health
→ 200 { "success": true, "message": "Restaurant backend is running" }

GET http://localhost:5000/api/v1/nothing-here
→ 404 { "success": false, "message": "Route not Found: ..." }
```

## Step A7 — Backend current status (honest)

| Item | Status |
|---|---|
| Express app + middleware + routing | ✅ done |
| Health API | ✅ done |
| 404 + global error handling | ✅ done |
| Environment config | ✅ done |
| MongoDB connection | ❌ NOT done — `config/database.js` is **empty**, Phase 3 next |
| Auth / modules / real APIs | ❌ empty folders only |
| Socket.IO | ❌ not started |

---

# 4. PART B — How the FRONTEND was created + every change (before → after)

The Flutter app **already existed** (built earlier with Supabase as its backend). The work
done since then was: **(1)** fix a version problem, **(2)** add the HTTP package,
**(3)** build the Node-connection layer, **(4)** keep all existing screens working.

## B1 — BEFORE vs AFTER: `frontend/pubspec.yaml` (only 2 changes)

**BEFORE:**

```yaml
environment:
  sdk: ^3.14.0-160.0.dev
```

**AFTER:**

```yaml
environment:
  sdk: ^3.13.0
```

**Why:** `flutter pub get` failed with:

```
Because resto requires SDK version ^3.14.0-160.0.dev, version solving failed.
```

Our installed Flutter ships Dart 3.13.x, so the constraint was lowered to match.

**Second change — added one dependency:**

```yaml
dependencies:
  cupertino_icons: ^1.0.8
  supabase_flutter: ^2.17.2
  flutter_riverpod: ^3.4.2
  go_router: ^18.0.0
  flutter_dotenv: ^6.0.1
  google_fonts: ^8.2.1
  geolocator: ^14.0.3
  geocoding: ^5.0.0
  http: ^1.2.2          # ← ADDED: this is what lets Flutter call the Node backend
```

After editing, run:

```bash
cd frontend
flutter pub get
```

## B2 — New files created (these are the "before → after" story)

### B2.1 `lib/core/config/api_config.dart` — NEW — backend address lives here

```dart
class ApiConfig {
  static const String host = 'localhost';
  static const int port = 5000;

  static String get baseUrl => 'http://$host:$port/api/v1';

  static const String healthPath = '/health';
  static String get healthUrl => '$baseUrl$healthPath';
}
```

**Why a whole file for a URL?** One single place to change when we deploy to a real server,
or when testing from a real phone (see the host rules below).

| Run target | `host` value to use |
|---|---|
| Chrome / Windows / iOS simulator | `localhost` |
| **Android emulator** | `10.0.2.2` (emulator's alias for your PC) |
| **Physical Android phone** | your PC's LAN IP, e.g. `192.168.1.10` (same Wi-Fi!) |

### B2.2 `lib/core/network/api_client.dart` — NEW — the HTTP helper

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import '../config/api_config.dart';

class ApiClient {
  ApiClient({http.Client? client}) : _client = client ?? http.Client();
  final http.Client _client;

  Uri _uri(String path, [Map<String, String>? query]) {
    final normalized = path.startsWith('/') ? path : '/$path';
    return Uri.parse('${ApiConfig.baseUrl}$normalized').replace(
      queryParameters: query,
    );
  }

  Future<Map<String, dynamic>> get(String path,
      {Map<String, String>? query, Map<String, String>? headers}) async {
    final response = await _client.get(
      _uri(path, query),
      headers: {'Content-Type': 'application/json', ...?headers},
    );
    return _decode(response);
  }

  Future<Map<String, dynamic>> post(String path,
      {Map<String, dynamic>? body, Map<String, String>? headers}) async {
    final response = await _client.post(
      _uri(path),
      headers: {'Content-Type': 'application/json', ...?headers},
      body: body == null ? null : jsonEncode(body),
    );
    return _decode(response);
  }

  Map<String, dynamic> _decode(http.Response response) {
    final raw = response.body.isEmpty ? '{}' : response.body;
    final decoded = jsonDecode(raw);

    if (decoded is! Map<String, dynamic>) {
      throw ApiException(
        statusCode: response.statusCode,
        message: 'Unexpected response format from server',
      );
    }
    if (response.statusCode < 200 || response.statusCode >= 300) {
      throw ApiException(
        statusCode: response.statusCode,
        message: decoded['message']?.toString() ?? 'Request failed',
        data: decoded,
      );
    }
    return decoded;
  }

  void close() => _client.close();
}

class ApiException implements Exception {
  ApiException({required this.statusCode, required this.message, this.data});
  final int statusCode;
  final String message;
  final Map<String, dynamic>? data;

  @override
  String toString() => 'ApiException($statusCode): $message';
}
```

**What you get for free by using it:**
* base URL is automatically prepended — call `_client.get('/health')`, not the full URL
* JSON body encoding/decoding handled
* non-2xx responses throw a clean `ApiException` with the server's `message`
* works for **every future endpoint** — auth, restaurants, cart, orders — one pattern forever

### B2.3 `lib/data/repositories/backend_health_repository.dart` — NEW — health check logic

```dart
import '../../core/network/api_client.dart';

class BackendHealthRepository {
  BackendHealthRepository({ApiClient? client}) : _client = client ?? ApiClient();
  final ApiClient _client;

  Future<BackendHealthResult> checkHealth() async {
    try {
      final json = await _client.get('/health');
      final success = json['success'] == true;
      final message = json['message']?.toString() ?? 'No message from backend';

      return BackendHealthResult(ok: success, message: message, raw: json);
    } on ApiException catch (e) {
      return BackendHealthResult(ok: false, message: e.message, statusCode: e.statusCode);
    } catch (e) {
      return BackendHealthResult(
        ok: false,
        message: 'Cannot reach backend. Is Node running on port 5000?\n$e',
      );
    }
  }
}

class BackendHealthResult {
  const BackendHealthResult({required this.ok, required this.message,
      this.statusCode, this.raw});
  final bool ok;
  final String message;
  final int? statusCode;
  final Map<String, dynamic>? raw;
}
```

**Pattern to copy for every future feature:** repositories own API calls; screens never call
`ApiClient` directly.

### B2.4 `lib/features/connection/backend_connection_page.dart` — NEW — the visual test screen

A screen that on startup calls the repository, shows the API URL, a spinner, then a big
green **Connected ✓** or red **Not connected** with the error message, and a
"Test again" button. (Full code is in the file — it's plain Flutter, nothing tricky.)

### B2.5 `lib/main_backend_check.dart` — NEW — alternate app entry point

```dart
/// Run with:
///   flutter run -d chrome -t lib/main_backend_check.dart
```

Same as `main.dart` (Supabase still initialized) but opens the **BackendConnectionPage**
first, with a floating "Open App" button that pushes `RestaurantMainPage` (the normal app).

### B2.6 `lib/main.dart` — the NORMAL entry (unchanged behaviour)

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();

  await Supabase.initialize(
    url: SupabaseConfig.url,
    anonKey: SupabaseConfig.publishableKey,
  );

  runApp(const ProviderScope(child: RestaurantApp()));
}
```

## B3 — What did NOT change (important!)

* All existing screens (`home`, `search`, `dineout`, `cart`, `draft`, `profile`,
  `restaurant details`) and their Supabase queries are **untouched** — they still read
  from Supabase.
* `lib/app/app.dart`, theme, navbar widgets — untouched.
* `supabase_config.dart` — untouched (URL + publishable key, legacy).

## B4 — Frontend files that still use Supabase (future migration list)

| File | What it fetches from Supabase today |
|---|---|
| `features/home/home_page.dart` | restaurants list + food items |
| `features/search/search_restaurant_page.dart` | search results |
| `features/cart/cart_page.dart` | cart + cart_items tables |
| `features/dineout/dineout_page.dart`, `dineout_selection.dart` | dineout data |
| `features/restaurant/restaurant_details_page.dart` | branches, categories, items |
| `data/repositories/restaurant_repository.dart` | restaurants table |

When the backend `restaurants`, `menu`, `cart` modules are ready, we swap these one file at
a time to use `ApiClient` — without changing the UI code.

## B5 — Run frontend + backend together

Terminal 1:

```bash
cd backend
npm run dev
```

Terminal 2:

```bash
cd frontend
flutter pub get
flutter run -d chrome -t lib/main_backend_check.dart   # connection test screen
# or
flutter run -d chrome                                  # normal app
```

Expected: green **Connected** on the test page. That single screen proves the whole stack.

---

# 5. PART C — How frontend connects to backend (the bridge)

The connection is just **HTTP + JSON**. Here is the exact journey of one request:

```
BackendConnectionPage (screen)
      │ initState()
      ▼
BackendHealthRepository.checkHealth()
      │
      ▼
ApiClient.get('/health')
      │  builds: http://localhost:5000/api/v1 + /health
      ▼
HTTP GET ───────────────────────►  Node.js :5000
                                   helmet → cors → json parser
                                   routes/index.js
                                   health.routes.js handler
      ◄──────────────────────────  200 + {"success":true,"message":"..."}
      ▼
_decode() checks status code, returns Map
      ▼
Repository wraps into BackendHealthResult(ok: true)
      ▼
setState() → screen shows green "Connected"
```

**Future features follow the exact same path** — only the path string and repository change:

```dart
final client = ApiClient();
final data = await client.get('/restaurants');          // GET
final res  = await client.post('/cart/items', body: {...}); // POST
```

On the Node side, each new module plugs into the same pipe:

```
/api/v1/restaurants → routes/index.js → modules/restaurants/restaurants.routes.js
                    → controller → service → model (Mongoose) → MongoDB
```

---

# 6. PART D — How WE will share the work (Git rules for 2 devs)

## D0 — ⚠️ CRITICAL first step before pushing (whoever pushes first)

The repo root `.gitignore` currently ignores only Flutter build files. The `backend/` folder
is still **untracked**, and its `.gitignore` is **empty**. If we `git add` blindly we will
commit **node_modules (thousands of files)** and **the secret .env**. Before the first
backend commit, the root `.gitignore` must gain:

```gitignore
node_modules/
backend/.env
*.log
.DS_Store
```

(and verify with `git status` that `backend/.env` and `backend/node_modules/` are NOT listed).
`.env.example`, `package.json`, `package-lock.json` DO get committed.

## D1 — Current repo state (what the teammate will receive)

| Item | Status |
|---|---|
| Git branch | `main` |
| Committed | old Flutter app (when it lived at repo root), moved into `frontend/`, Docs |
| **Uncommitted** | the whole `backend/`, the 5 new Flutter connection files, `pubspec.yaml` changes, `Docs/COMPLETE-PROJECT-GUIDE.md`, this file |

So the very first team action: **commit & push everything above (after D0)** so both of us
start from the same point.

## D2 — One-time setup for Developer #2

```bash
# get Node.js 18+ (we use v22) and Flutter (matching Dart 3.13.x)
git clone <repo-url>
cd resto

# backend
cd backend
npm install
copy .env.example .env        # then ask Dev#1 for real values via private chat
npm run dev                   # → Server running on port 5000

# frontend (new terminal)
cd ../frontend
flutter pub get
flutter doctor                # fix anything red
flutter run -d chrome -t lib/main_backend_check.dart
```

## D3 — The daily loop (memorize this)

```bash
# 1. start the day — get latest
git checkout main
git pull origin main

# 2. NEVER code directly on main — make a branch per task
git checkout -b feature/orders-module        # backend dev
git checkout -b feature/home-api-migration   # flutter dev

# 3. small commits, meaningful messages
git add src/modules/orders
git commit -m "orders: add order model and create-order endpoint"

# 4. push your branch
git push -u origin feature/orders-module

# 5. open a Pull Request on GitHub → other dev reviews → merge to main

# 6. next morning: pull main again and repeat
```

**Why branches + PRs?** `main` stays always-working. Mistakes stay inside the branch.
The reviewer (us) catches issues before they touch everyone.

## D4 — Avoiding conflicts (the rules that actually matter)

1. **Own your folder.** Backend dev edits only `backend/**`, Flutter dev only `frontend/**`
   (full ownership map in Part G).
2. **Never edit the same file at the same time.** The few shared files
   (`routes/index.js` when both add routes? no — backend-only; `api_config.dart` — both may
   need it → coordinate in chat, tiny edits, merge fast).
3. **Pull before you push.** Always `git pull origin main` (or rebase your branch) before
   pushing — this shrinks conflicts to nearly zero.
4. **`.env` is NEVER committed, NEVER messaged as plain text if it has real secrets.**
   Only `.env.example` changes go to Git; real values travel by private chat/password manager.
5. **Commit small and often.** One logical change per commit → conflicts, when they happen,
   are trivial.
6. **Big schema/route decisions are announced in chat first** so the other dev isn't surprised
   by breaking changes.

## D5 — If a conflict happens anyway

```bash
git pull origin main
# Git says: CONFLICT in file X
```

Open file X, look for the markers:

```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> origin/main
```

Keep the correct combined result, delete the markers, then:

```bash
git add <file>
git commit          # finishes the merge
```

For `.env`-style or generated files (`pubspec.lock`, `package-lock.json`) — don't hand-merge;
regenerate instead: `flutter pub get` / `npm install`.

---

# 7. PART E — Two developers, ONE MongoDB database

Both of us will connect to the **same database** during development. Here's the safe way.

## E1 — Recommended setup: MongoDB Atlas (cloud, free tier M0)

One of us (Dev #1) creates it once:

1. Register at **mongodb.com/atlas** → Create free cluster (M0).
2. **Database Access** → create a DB user, e.g. username `resto-dev`, strong password.
   For a 2-person team one shared DB user is simplest.
3. **Network Access** → add IP `0.0.0.0/0` (allow from anywhere) — acceptable for dev
   because security comes from the DB credentials; tighten later.
4. **Database** → create database `resto` (dev data lives here).
5. **Connect → Drivers → Node.js** → copy the connection string, it looks like:

```
mongodb+srv://resto-dev:<password>@cluster0.xxxxx.mongodb.net/resto?retryWrites=true&w=majority
```

6. Put it in `backend/.env`:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb+srv://resto-dev:<real-password>@cluster0.xxxxx.mongodb.net/resto?retryWrites=true&w=majority
```

and ONLY a placeholder in `.env.example`:

```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb+srv://USER:PASSWORD@cluster0.xxxxx.mongodb.net/resto?retryWrites=true
```

7. Share the **real** URI with the teammate privately (password manager, WhatsApp DM, call) —
   never in a commit, never in a group chat, never in the README.

Dev #2 then pastes the same URI into their own local `backend/.env` — done, both machines
now read/write the **same database**.

## E2 — How the connection code will work (Phase 3 preview)

`src/config/database.js` is currently **empty**. It will gain roughly:

```js
const mongoose = require("mongoose");
const env = require("./env");

const connectDB = async () => {
  await mongoose.connect(env.mongoUri);   // env.js will expose process.env.MONGODB_URI
  console.log("MongoDB connected");
};

module.exports = connectDB;
```

and `server.js` will call `connectDB()` before `app.listen(...)`. (We'll build this together
— this snippet is just so you know the shape.)

## E3 — Rules for two people hammering one database

1. **Prefix collections by feature** so we never collide:
   `users`, `restaurants`, `menu_items`, `orders`, `carts`… The Mongoose model decides the
   collection name — **the backend dev owns model files**; the Flutter dev never invents
   collection names.
2. **One owner per model.** Models (`*.model.js`) are edited by one person at a time.
   Schema changes = announce in chat first, because both apps depend on the shape.
3. **Never drop collections/databases** — not even "to clean up". If test data is junk,
   create clearly-named throwaway docs (`name: "TEST - delete me"`), or ask before wiping.
4. **Test data is fine.** Atlas free tier has plenty of space for dev junk. Dirty data is
   better than deleted data.
5. **Keep IDs portable.** Documents get `_id` automatically — Flutter should treat ids as
   opaque strings (`json['_id']`), never parse them.
6. **MongoDB Compass** (free GUI) — both of us install it, connect with the same URI, and
   can visually inspect the shared data. Great for debugging "why is the app showing this?".
7. **Backups:** Atlas free tier keeps basic snapshots; for risky operations (bulk edits) do
   an export first (`Compass → Export Collection`).
8. **Later, if we outgrow sharing one login:** create a second Atlas DB user with
   readWrite on the same database — same URI pattern, different credentials, zero code change.

---

# 8. PART F — ONE Postman for testing endpoints together

Postman is how we both test the API **without running the Flutter app**. Goal: one shared
collection that always matches the real backend.

## F1 — Recommended: a shared Postman workspace

1. Both create free **Postman** accounts.
2. Dev #1 creates a **Workspace** → `Resto Team` → Invite `Developer #2` by email
   (free plan allows a small team workspace).
3. Inside, create **Collection: Resto API v1**.
4. Everything saved in a team workspace syncs automatically to both accounts — one source
   of truth, always up to date for both of us.

**Fallback if workspace invite is a problem:** Dev #1 selects the collection →
`Export (v2.1)` → commit the JSON at `postman/resto-api.postman_collection.json` in the repo;
Dev #2 imports it. Environment JSON exported the same way. Whoever changes endpoints,
re-exports and commits.

## F2 — Create a Postman Environment (so URLs are never hardcoded)

Workspace → Environments → **Resto Local**:

| Variable | Initial value | Current value |
|---|---|---|
| `base_url` | `http://localhost:5000/api/v1` | same |

In requests use `{{base_url}}/health`. When we deploy to a server someday, we make a second
environment `Resto Production` and change only the variable.

## F3 — Requests to create today (matches the real backend)

```
GET   {{base_url}}/health          → 200 {"success": true, "message": "Restaurant backend is running"}
GET   {{base_url}}/anything-else   → 404 {"success": false, "message": "Route not Found: ..."}
```

## F4 — Rules for shared Postman usage

1. **New endpoint = new request in the collection, same day.** Folder per module
   (`Health`, `Auth`, `Restaurants`, `Cart`, `Orders`…).
2. Name requests by verb + path: `POST /auth/register`, `GET /restaurants/:id`.
3. Use the **Examples** tab to store a sample real response under each request —
   the other dev instantly sees the shape without running anything.
4. Don't rename or delete each other's requests in the shared collection; add a new version.
5. Environment variables (`{{token}}` for auth later) keep secrets out of the collection;
   put tokens in *current value* only (it stays local to your Postman).

## F5 — Testing a brand-new endpoint (our ritual)

```
Backend dev:  code the endpoint → run in Postman → save request + example response in shared collection → push code
Flutter dev:  open Postman → run the request to see the contract → build repository method with ApiClient
```

Postman is our **shared contract document** — the Flutter dev can build UI against endpoints
that exist in Postman even before integrating.

---

# 9. PART G — Who works on which files (ownership map)

**Dev BE = backend developer, Dev FE = Flutter developer.**

| Area | Path | Owner | Notes |
|---|---|---|---|
| Express app, middleware, config | `backend/src/**` (except routes/index.js edits by agreement) | **Dev BE** | |
| New API modules | `backend/src/modules/<name>/**` | **Dev BE** | FE never edits |
| Route registration | `backend/src/routes/index.js` | **Dev BE** | one line per module |
| Backend env | `backend/.env`, `.env.example` | **Dev BE** creates; values shared privately | |
| Backend docs | `backend/docs/*.md` | **Dev BE** | |
| Flutter screens / widgets | `frontend/lib/features/**`, `frontend/lib/core/widgets/**` | **Dev FE** | |
| Flutter theme/app shell | `frontend/lib/app/**` | **Dev FE** | |
| Flutter repositories | `frontend/lib/data/repositories/**` | **Dev FE** | calls endpoints agreed in Postman |
| `frontend/lib/core/config/api_config.dart` | shared-ish | **Dev FE** (BE may request URL changes in chat) | tiny file, low risk |
| `frontend/pubspec.yaml` | **Dev FE** | BE never adds Flutter packages | |
| `postman/` collection exports | **either** (whoever changes endpoints re-exports) | | |
| `Docs/` | **either** | | |
| `.gitignore` (root) | **either**, announce in chat | | |
| MongoDB models (`*.model.js`) | **Dev BE** | schema changes announced first | |

**Coordination protocol when BE ships a new endpoint:**
BE → endpoint live + Postman request saved → ping FE with path & sample JSON →
FE adds repository method + UI. FE never guesses endpoint shapes.

---

# 10. Known quirks / typos to fix later

Do **not** silently fix these while doing other work — we'll do one cleanup commit together:

| # | Where | Quirk | Why it still works / plan |
|---|---|---|---|
| 1 | `backend/src/middleware/error.middleware.js` | `stausCode` misspelled (variable + property) | consistent inside the file, so it runs; will rename to `statusCode` |
| 2 | Folder naming | docs mention `src/middlewares/`, real folder is `src/middleware/` | real folder wins; docs are historical |
| 3 | `backend/.gitignore` | file is **empty** | must be filled before first backend push (see D0) — CRITICAL |
| 4 | `backend/package.json` | `"main": "src/server.js"` fine, older docs said `"main": "server.js"` | already correct now |
| 5 | `frontend/lib/core/config/supabase_config.dart` | Supabase URL + publishable key hardcoded | publishable key is public-ish; fine for now, will move to dotenv-style config later |
| 6 | `backend/src/config/database.js` | empty file | Phase 3 will fill it (see E2) |
| 7 | Root `.gitignore` | doesn't yet ignore `node_modules/` or `.env` | fix together with #3 |

---

# 11. Quick command cheat sheet

```powershell
# ---------- BACKEND ----------
cd backend
npm install                # after clone or after pulling new packages
npm run dev                # start dev server (auto-restart)  → :5000
npm start                  # plain start

# test health in PowerShell
Invoke-RestMethod http://localhost:5000/api/v1/health

# ---------- FRONTEND ----------
cd frontend
flutter pub get            # after clone or pubspec change
flutter doctor             # environment check
flutter devices            # list targets
flutter run -d chrome -t lib/main_backend_check.dart   # connection test screen
flutter run -d chrome                                  # normal app

# ---------- GIT DAILY ----------
git checkout main && git pull origin main
git checkout -b feature/<name>
git add <specific files>
git commit -m "area: what and why"
git push -u origin feature/<name>
# → open Pull Request → review → merge

# ---------- WHEN LOCKFILE CONFLICTS ----------
npm install                # regenerate package-lock.json
flutter pub get            # regenerate pubspec.lock
```

---

# 12. Mental model — remember only these 5 lines

1. **Flutter = face. Node = brain. MongoDB = memory.** They speak HTTP+JSON.
2. Everything starts at `backend/src/server.js` and `frontend/lib/main.dart`.
3. New backend feature = new folder in `modules/` + one line in `routes/index.js`.
4. New frontend data = new repository method using `ApiClient` + endpoint agreed in Postman.
5. Work on branches, pull before push, `.env` never committed, MongoDB shared but models owned.

**Welcome aboard 🚀** — first joint tasks: (1) fix `.gitignore` + push everything,
(2) Phase 3: MongoDB connection, (3) build the `restaurants` module API, (4) point Flutter
home screen to Node instead of Supabase.