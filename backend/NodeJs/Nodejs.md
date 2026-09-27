# Node.js Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** Important Node.js concepts + commonly asked interview questions
> **Goal:** Understand Node.js fundamentals and explain backend concepts confidently in interviews.

---

# 1. What is Node.js?

Node.js is a **JavaScript runtime environment** that allows JavaScript to run outside the browser.

It is built on Google's **V8 JavaScript engine**.

```text
Browser
   ↓
JavaScript → Browser APIs

Node.js
   ↓
JavaScript → Node.js APIs → Operating System
```

Example:

```js
console.log("Hello from Node.js");
```

You can run it using:

```bash
node app.js
```

### Interview Point

> Node.js is not a programming language or framework. It is a JavaScript runtime environment.

---

# 2. Why is Node.js used for backend development?

Node.js is commonly used for:

* REST APIs
* Web applications
* Real-time applications
* Authentication systems
* File processing
* Microservices
* Streaming applications

Major advantages:

* JavaScript on the server
* Asynchronous programming
* Non-blocking I/O
* Large npm ecosystem
* Good performance for I/O-heavy applications

---

# 3. What is the V8 Engine?

V8 is Google's JavaScript engine.

Node.js uses V8 to execute JavaScript.

```text
JavaScript
    ↓
V8 Engine
    ↓
Machine Code
```

V8 is primarily responsible for executing JavaScript code efficiently.

---

# 4. Is Node.js single-threaded?

Node.js executes JavaScript code primarily on a **single main thread**.

However, Node.js can handle many concurrent operations using:

* Event loop
* Asynchronous APIs
* OS capabilities
* libuv
* Worker threads for certain CPU-intensive workloads

Therefore:

> Single-threaded JavaScript execution does not mean Node.js can handle only one request at a time.

---

# 5. What is the Event Loop?

The Event Loop allows Node.js to handle asynchronous operations without blocking the main JavaScript execution thread.

Basic idea:

```text
Request
   ↓
Node.js
   ↓
Start asynchronous operation
   ↓
Continue executing other work
   ↓
Operation completes
   ↓
Callback / Promise continuation
   ↓
Event Loop
   ↓
JavaScript executes callback
```

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timer");
}, 0);

console.log("End");
```

Output:

```text
Start
End
Timer
```

### Interview Point

> The Event Loop coordinates asynchronous callbacks and allows Node.js to handle concurrent I/O efficiently.

---

# 6. What is libuv?

libuv is a library used by Node.js to provide asynchronous I/O capabilities.

It helps Node.js work with:

* File system operations
* Networking
* Timers
* Asynchronous operations
* Thread pool

Simplified architecture:

```text
JavaScript
    ↓
Node.js APIs
    ↓
libuv
    ↓
OS / Thread Pool
```

---

# 7. What is non-blocking I/O?

Non-blocking I/O means Node.js can start an I/O operation and continue doing other work instead of waiting synchronously for the operation to finish.

Example:

```js
const fs = require("fs");

fs.readFile("data.txt", "utf8", (err, data) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(data);
});

console.log("Reading file...");
```

The program can continue while the file operation is being completed.

---

# 8. What is blocking vs non-blocking code?

### Blocking

The next operation waits until the current operation completes.

```js
const fs = require("fs");

const data = fs.readFileSync("data.txt", "utf8");

console.log(data);
console.log("Next operation");
```

### Non-blocking

The operation happens asynchronously.

```js
const fs = require("fs");

fs.readFile("data.txt", "utf8", (err, data) => {
  console.log(data);
});

console.log("Next operation");
```

### Important Point

For server applications, asynchronous/non-blocking APIs are generally preferred for I/O operations.

---

# 9. What is npm?

npm stands for **Node Package Manager**.

It is used to:

* Install packages
* Manage dependencies
* Run scripts
* Publish packages

Example:

```bash
npm install express
```

---

# 10. What is `package.json`?

`package.json` contains project metadata and dependency information.

Example:

```json
{
  "name": "backend",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "^5.0.0"
  }
}
```

It can contain:

* Project name
* Version
* Scripts
* Dependencies
* Dev dependencies
* Entry-point information
* Other project metadata

---

# 11. Difference between dependencies and devDependencies

### dependencies

Required for the application to run.

```bash
npm install express
```

### devDependencies

Primarily required during development.

```bash
npm install --save-dev nodemon
```

Example:

```json
{
  "dependencies": {
    "express": "^5.0.0"
  },
  "devDependencies": {
    "nodemon": "^3.0.0"
  }
}
```

---

# 12. What is `node_modules`?

`node_modules` contains installed npm packages and their dependencies.

For example:

```text
project/
├── node_modules/
├── package.json
├── package-lock.json
└── server.js
```

Usually, `node_modules` should **not** be committed to Git.

Add it to `.gitignore`:

```text
node_modules/
```

---

# 13. What is `package-lock.json`?

`package-lock.json` records the resolved versions of packages and their dependency tree.

It helps keep installations consistent across environments.

Usually:

```text
package.json
package-lock.json
```

should be committed to Git for an application project.

---

# 14. What are CommonJS modules?

CommonJS is one module system supported by Node.js.

Import:

```js
const express = require("express");
```

Export:

```js
module.exports = app;
```

Example:

```js
// math.js

function add(a, b) {
  return a + b;
}

module.exports = add;
```

```js
// app.js

const add = require("./math");

console.log(add(10, 20));
```

---

# 15. What are ES Modules?

Node.js also supports the ES Module syntax.

Import:

```js
import express from "express";
```

Export:

```js
export default app;
```

Named export:

```js
export { add };
```

The project configuration determines which module system is being used.

---

# 16. CommonJS vs ES Modules

| CommonJS                          | ES Modules                        |
| --------------------------------- | --------------------------------- |
| `require()`                       | `import`                          |
| `module.exports`                  | `export`                          |
| Traditional Node.js module system | JavaScript standard module system |
| Common in older Node.js projects  | Common in modern projects         |

Example:

```js
const express = require("express");
```

vs.

```js
import express from "express";
```

### Interview Point

> Don't mix module systems carelessly in the same project.

---

# 17. What are Node.js core modules?

Node.js provides built-in modules that don't need to be installed using npm.

Examples:

```text
fs
path
http
os
url
events
crypto
stream
```

Example:

```js
const path = require("path");

console.log(path.join("src", "server.js"));
```

---

# 18. What is the `fs` module?

`fs` stands for **File System**.

It is used to work with files and directories.

Example:

```js
const fs = require("fs");

fs.writeFile(
  "message.txt",
  "Hello Node.js",
  (err) => {
    if (err) {
      console.error(err);
      return;
    }

    console.log("File created");
  }
);
```

Common methods:

```text
readFile()
writeFile()
appendFile()
unlink()
mkdir()
readdir()
```

---

# 19. What is the `path` module?

The `path` module provides utilities for working with file and directory paths.

```js
const path = require("path");

const filePath = path.join(
  __dirname,
  "public",
  "index.html"
);

console.log(filePath);
```

Common methods:

```text
path.join()
path.resolve()
path.basename()
path.dirname()
path.extname()
```

---

# 20. What is the `http` module?

The `http` module can create an HTTP server without Express.

```js
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, {
    "Content-Type": "text/plain"
  });

  res.end("Server is working");
});

server.listen(5000, () => {
  console.log("Server running");
});
```

Express is built on top of Node's HTTP capabilities.

---

# 21. How do you create a basic Node.js server?

Using the built-in `http` module:

```js
const http = require("http");

const server = http.createServer((req, res) => {
  res.end("Hello World");
});

server.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

---

# 22. What is an environment variable?

Environment variables store configuration values outside the source code.

Example:

```text
PORT=5000
MONGO_URI=your_database_url
JWT_SECRET=your_secret
```

In Node.js:

```js
console.log(process.env.PORT);
```

For `.env` files, projects commonly use the `dotenv` package.

```js
require("dotenv").config();

console.log(process.env.PORT);
```

### Important Point

Never commit real secrets to GitHub.

---

# 23. What is `process.env`?

`process.env` provides access to environment variables.

```js
const port = process.env.PORT || 5000;
```

Example:

```text
PORT=5000
```

Then:

```js
console.log(process.env.PORT);
```

returns the configured environment value.

---

# 24. What is `process` in Node.js?

`process` is a global object that provides information and control over the current Node.js process.

Examples:

```js
console.log(process.env);
console.log(process.pid);
console.log(process.version);
```

It can also be used to terminate a process:

```js
process.exit(1);
```

---

# 25. What is a callback?

A callback is a function passed to another function to be executed later.

```js
function greet(name, callback) {
  callback(`Hello ${name}`);
}

greet("Veera", (message) => {
  console.log(message);
});
```

Callbacks were widely used for asynchronous Node.js APIs.

---

# 26. What is callback hell?

Callback hell happens when many nested callbacks make code difficult to read and maintain.

Example:

```js
doTask1(() => {
  doTask2(() => {
    doTask3(() => {
      doTask4(() => {
        // ...
      });
    });
  });
});
```

Promises and `async/await` provide cleaner approaches.

---

# 27. What are Promises?

A Promise represents the eventual completion or failure of an asynchronous operation.

States:

```text
Pending
   ↓
Fulfilled

or

Pending
   ↓
Rejected
```

Example:

```js
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise.then((result) => {
  console.log(result);
});
```

---

# 28. What is `async/await`?

`async/await` provides a cleaner way to work with Promises.

```js
async function getData() {
  try {
    const response = await fetch(
      "https://example.com/api/users"
    );

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
```

### Interview Point

`async/await` does not make asynchronous operations synchronous. It provides cleaner syntax for working with Promises.

---

# 29. How do you handle errors in Node.js?

For synchronous code:

```js
try {
  // code
} catch (error) {
  console.error(error);
}
```

For async/await:

```js
try {
  const data = await getData();
} catch (error) {
  console.error(error);
}
```

For callbacks:

```js
fs.readFile("file.txt", (err, data) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(data);
});
```

Express applications generally use centralized error-handling middleware.

---

# 30. What are Streams?

Streams allow data to be processed gradually instead of loading the entire data set into memory at once.

Types include:

```text
Readable
Writable
Duplex
Transform
```

Example:

```js
const fs = require("fs");

const stream = fs.createReadStream("large-file.txt");

stream.on("data", (chunk) => {
  console.log(chunk);
});
```

Useful for:

* Large files
* Video/audio
* Network data
* File uploads/downloads

---

# 31. What is a Buffer?

A Buffer is a Node.js object used to work with raw binary data.

Example:

```js
const buffer = Buffer.from("Hello");

console.log(buffer);
console.log(buffer.toString());
```

Buffers are commonly encountered when working with:

* Files
* Streams
* Network data
* Binary content

---

# 32. What is EventEmitter?

`EventEmitter` allows objects to emit and listen for custom events.

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("login", (username) => {
  console.log(`${username} logged in`);
});

emitter.emit("login", "Veera");
```

Important methods:

```text
on()
emit()
once()
off()
```

---

# 33. What is middleware in Node.js?

Middleware is primarily an **Express concept**, where functions execute during the request-response lifecycle.

A typical middleware receives:

```js
(req, res, next)
```

Example:

```js
app.use((req, res, next) => {
  console.log(req.method, req.url);

  next();
});
```

`next()` passes control to the next middleware or route handler.

---

# 34. What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It controls which origins are allowed to access resources from a server through browser requests.

In Express:

```js
const cors = require("cors");

app.use(cors());
```

A production application should normally configure allowed origins rather than blindly allowing every origin.

---

# 35. What is REST API?

REST is an architectural style commonly used to build HTTP APIs.

Typical operations:

```text
GET     → Read
POST    → Create
PUT     → Replace/update
PATCH   → Partial update
DELETE  → Delete
```

Example:

```text
GET    /api/users
GET    /api/users/123
POST   /api/users
PATCH  /api/users/123
DELETE /api/users/123
```

---

# 36. What is the request-response lifecycle?

A typical Node.js + Express API flow:

```text
Client
  ↓
HTTP Request
  ↓
Server
  ↓
Middleware
  ↓
Route
  ↓
Controller
  ↓
Service / Business Logic
  ↓
Database
  ↓
Response
  ↓
Client
```

Example:

```text
Flutter / React
      ↓
POST /api/users
      ↓
Express
      ↓
Auth Middleware
      ↓
User Controller
      ↓
User Service
      ↓
MongoDB
      ↓
JSON Response
```

---

# 37. What is `nodemon`?

`nodemon` automatically restarts the Node.js application when files change during development.

Install:

```bash
npm install --save-dev nodemon
```

Example:

```json
{
  "scripts": {
    "dev": "nodemon server.js"
  }
}
```

Run:

```bash
npm run dev
```

---

# 38. What is the difference between Node.js and Express.js?

| Node.js                           | Express.js                              |
| --------------------------------- | --------------------------------------- |
| JavaScript runtime                | Web framework                           |
| Provides runtime and core APIs    | Provides routing and middleware         |
| Can create HTTP servers           | Simplifies HTTP application development |
| Lower-level                       | Higher-level                            |
| Uses modules such as `http`, `fs` | Built on Node.js                        |

Simple relationship:

```text
Node.js
   ↓
Express.js
   ↓
REST API
```

---

# 39. What are Worker Threads?

Worker Threads allow JavaScript code to run in separate threads.

They are useful for **CPU-intensive tasks** that could otherwise block the main JavaScript thread.

Examples:

* Heavy calculations
* CPU-intensive processing
* Certain data transformations

For normal database/API I/O, asynchronous Node.js APIs are usually sufficient.

---

# 40. How can Node.js applications be made more secure?

Important practices:

```text
Validate input
Hash passwords
Use HTTPS
Protect secrets
Configure CORS
Use security headers
Rate-limit sensitive endpoints
Validate authentication
Verify JWTs
Implement authorization
Sanitize/validate data
Keep dependencies updated
Handle errors safely
```

For an Express application, security middleware such as Helmet and rate-limiting solutions are commonly used as part of a broader security strategy.

---

# 41. What is clustering in Node.js?

Clustering allows multiple Node.js processes to run so an application can use multiple CPU cores.

Conceptually:

```text
                 Load
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     Worker 1  Worker 2  Worker 3
```

Each worker runs its own Node.js process.

For modern deployments, process managers and container/orchestration platforms may also be used to scale Node.js applications.

---

# 42. What is the difference between CPU-intensive and I/O-intensive tasks?

### I/O-intensive

The application spends time waiting for:

* Database
* File system
* Network
* External APIs

Node.js is well suited to handling many concurrent I/O operations.

### CPU-intensive

The application spends significant time performing computation.

Examples:

* Large mathematical calculations
* Image processing
* Video processing
* Complex data processing

Long CPU-intensive work can block the main JavaScript thread, so worker threads or separate services may be appropriate.

---

# 43. What is a good Node.js backend folder structure?

A scalable backend can be organised like:

```text
backend/
├── src/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── utils/
│   ├── app.js
│   └── server.js
│
├── .env
├── .gitignore
├── package.json
└── package-lock.json
```

### Responsibility

```text
routes       → API endpoints
controllers  → Request/response handling
services     → Business logic
models       → Database models
middleware   → Request processing/authentication
config       → Configuration
utils        → Reusable utilities
app.js       → Express application
server.js    → Start server
```

---

# 44. What is the difference between `app.js` and `server.js`?

A common architecture separates application configuration from server startup.

### `app.js`

```js
const express = require("express");

const app = express();

app.use(express.json());

module.exports = app;
```

### `server.js`

```js
const app = require("./app");

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

This separation makes the application easier to test and organise.

---

# 45. How do you build a clean Node.js API?

A common flow:

```text
Request
   ↓
Route
   ↓
Middleware
   ↓
Controller
   ↓
Service
   ↓
Model
   ↓
Database
```

Example:

```text
POST /api/products
        ↓
productRoutes
        ↓
authMiddleware
        ↓
productController
        ↓
productService
        ↓
Product Model
        ↓
MongoDB
```

This separation keeps responsibilities clear and makes a backend easier to maintain.

---

# Node.js Interview Revision Checklist

## Core

* [ ] What is Node.js?
* [ ] Node.js vs JavaScript
* [ ] Node.js vs Express.js
* [ ] V8 engine
* [ ] Single-threaded model
* [ ] Event Loop
* [ ] libuv
* [ ] Non-blocking I/O
* [ ] Blocking vs non-blocking

## npm & Modules

* [ ] npm
* [ ] package.json
* [ ] package-lock.json
* [ ] node_modules
* [ ] dependencies
* [ ] devDependencies
* [ ] CommonJS
* [ ] ES Modules
* [ ] Core modules

## Node.js APIs

* [ ] `fs`
* [ ] `path`
* [ ] `http`
* [ ] `process`
* [ ] `process.env`
* [ ] Environment variables
* [ ] EventEmitter
* [ ] Streams
* [ ] Buffers

## Asynchronous Programming

* [ ] Callbacks
* [ ] Callback hell
* [ ] Promises
* [ ] async/await
* [ ] Error handling
* [ ] Event Loop

## Backend Concepts

* [ ] REST API
* [ ] HTTP methods
* [ ] Request-response lifecycle
* [ ] CORS
* [ ] Middleware
* [ ] Nodemon
* [ ] Worker Threads
* [ ] Clustering
* [ ] CPU-intensive vs I/O-intensive tasks

## Architecture

* [ ] Routes
* [ ] Controllers
* [ ] Services
* [ ] Models
* [ ] Middleware
* [ ] Config
* [ ] `app.js`
* [ ] `server.js`

---

# Final Node.js Interview Flow

You should be able to explain this clearly:

```text
Client
  ↓
HTTP Request
  ↓
Node.js Runtime
  ↓
Express Server
  ↓
Middleware
  ↓
Route
  ↓
Controller
  ↓
Service
  ↓
Database
  ↓
Response
  ↓
Client
```

And explain the core Node.js concept behind the server:

```text
Request
   ↓
Node.js
   ↓
Event Loop
   ↓
Non-blocking I/O
   ↓
Async Operation
   ↓
Callback / Promise
   ↓
Response
```

> **Main interview goal:** Don't just memorise Node.js definitions. Be able to explain how a real request travels through your backend and why Node.js can handle many I/O operations concurrently.
