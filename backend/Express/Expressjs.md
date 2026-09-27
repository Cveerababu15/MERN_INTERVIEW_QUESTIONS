# Express.js Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** Important Express.js concepts + commonly asked interview questions
> **Prerequisite:** Node.js

---

# 1. What is Express.js?

Express.js is a **web framework for Node.js** used to build:

* REST APIs
* Web servers
* Backend applications
* Middleware-based applications

Example:

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("Server is working");
});

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

### Interview Point

> Express.js is a lightweight web framework built on top of Node.js that simplifies routing, middleware, and HTTP application development.

---

# 2. Why do we use Express.js?

Without Express, Node.js can create an HTTP server using the built-in `http` module, but handling:

* Routes
* Middleware
* Request parsing
* Error handling
* API structure

would require more manual code.

Express simplifies these tasks.

---

# 3. Express.js vs Node.js

| Node.js                           | Express.js                      |
| --------------------------------- | ------------------------------- |
| JavaScript runtime                | Web framework                   |
| Provides core APIs                | Provides routing and middleware |
| Can create HTTP servers           | Simplifies API development      |
| Lower-level                       | Higher-level                    |
| Uses modules such as `http`, `fs` | Built on Node.js                |

```text
Node.js
   ↓
Express.js
   ↓
REST API
```

---

# 4. How do you create an Express application?

```js
const express = require("express");

const app = express();

app.listen(5000, () => {
  console.log("Server running");
});
```

`express()` creates an Express application instance.

---

# 5. What is `app.listen()`?

`app.listen()` starts the server and makes it listen for incoming requests on a port.

```js
app.listen(5000, () => {
  console.log("Server running on port 5000");
});
```

---

# 6. What is routing in Express?

Routing determines how the application responds to a particular HTTP method and URL.

```js
app.get("/users", (req, res) => {
  res.json({
    message: "Get users"
  });
});
```

Here:

```text
GET
/users
```

is the route.

---

# 7. What are HTTP methods commonly used with Express?

```text
GET     → Read
POST    → Create
PUT     → Replace/update
PATCH   → Partial update
DELETE  → Delete
```

Examples:

```js
app.get("/users", getUsers);

app.post("/users", createUser);

app.put("/users/:id", updateUser);

app.patch("/users/:id", updateUserPartially);

app.delete("/users/:id", deleteUser);
```

---

# 8. What is middleware?

Middleware is a function that runs during the request-response lifecycle.

It commonly receives:

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

# 9. What are the types of middleware?

Common categories include:

### Application-level

```js
app.use(...)
```

### Router-level

```js
router.use(...)
```

### Built-in

```js
express.json()
express.urlencoded()
express.static()
```

### Error-handling

```js
(err, req, res, next)
```

### Third-party

Examples:

```text
cors
helmet
morgan
```

---

# 10. What is `express.json()`?

It parses incoming requests containing JSON and makes the parsed data available through `req.body`.

```js
app.use(express.json());
```

Request:

```json
{
  "name": "Veera",
  "age": 21
}
```

Access:

```js
app.post("/users", (req, res) => {
  console.log(req.body);
});
```

---

# 11. What is `express.urlencoded()`?

It parses URL-encoded form data.

```js
app.use(express.urlencoded({ extended: true }));
```

It is commonly used when handling traditional HTML form submissions.

---

# 12. What is `express.static()`?

It serves static files such as:

* Images
* CSS
* JavaScript
* HTML
* Documents

Example:

```js
app.use(
  express.static("public")
);
```

A file inside:

```text
public/image.jpg
```

can then be served as a static resource.

---

# 13. What is `req`?

`req` represents the incoming HTTP request.

It contains information such as:

```text
req.params
req.query
req.body
req.headers
req.method
req.url
```

Example:

```js
app.get("/users", (req, res) => {
  console.log(req.method);
  console.log(req.headers);
});
```

---

# 14. What is `res`?

`res` represents the HTTP response sent back to the client.

Common methods:

```text
res.send()
res.json()
res.status()
res.redirect()
res.sendFile()
```

Example:

```js
res.status(200).json({
  message: "Success"
});
```

---

# 15. What is `req.params`?

Route parameters are values embedded in the URL path.

Example:

```js
app.get("/users/:id", (req, res) => {
  console.log(req.params.id);
});
```

Request:

```text
GET /users/101
```

Result:

```text
101
```

---

# 16. What is `req.query`?

Query parameters appear after `?` in the URL.

Example:

```text
GET /users?page=2&limit=10
```

Access:

```js
app.get("/users", (req, res) => {
  console.log(req.query.page);
  console.log(req.query.limit);
});
```

---

# 17. Difference between `req.params`, `req.query`, and `req.body`

| Type   | Example         | Access           |
| ------ | --------------- | ---------------- |
| Params | `/users/101`    | `req.params.id`  |
| Query  | `/users?page=2` | `req.query.page` |
| Body   | JSON request    | `req.body`       |

### Simple Rule

```text
URL path → params
URL ?key=value → query
Request data → body
```

---

# 18. What is `req.headers`?

Headers contain metadata sent with an HTTP request.

Example:

```js
app.get("/users", (req, res) => {
  console.log(req.headers);
});
```

A common authentication header is:

```text
Authorization: Bearer <token>
```

---

# 19. What is `res.json()`?

`res.json()` sends a JSON response.

```js
app.get("/user", (req, res) => {
  res.json({
    name: "Veera",
    role: "developer"
  });
});
```

---

# 20. What is `res.status()`?

It sets the HTTP status code.

```js
res.status(200).json({
  message: "Success"
});
```

Example:

```js
res.status(201).json({
  message: "User created"
});
```

---

# 21. What are common HTTP status codes?

```text
200 → OK
201 → Created
204 → No Content

400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
409 → Conflict
422 → Unprocessable Content

500 → Internal Server Error
```

### Important Difference

```text
401 → Authentication problem
403 → Authorization/permission problem
```

---

# 22. What is `express.Router()`?

`express.Router()` creates a modular route handler.

Example:

```js
const express = require("express");

const router = express.Router();

router.get("/", (req, res) => {
  res.json({
    message: "Users"
  });
});

module.exports = router;
```

Then:

```js
const userRoutes = require("./routes/userRoutes");

app.use("/api/users", userRoutes);
```

Now:

```text
GET /api/users
```

will reach the router.

---

# 23. Why use Express Router?

It keeps routes organised.

Instead of:

```text
app.js
  ↓
100+ routes
```

we can use:

```text
routes/
├── userRoutes.js
├── productRoutes.js
├── orderRoutes.js
└── authRoutes.js
```

This makes the application easier to maintain.

---

# 24. What is a controller?

A controller handles the request and response logic for a route.

Example:

```js
const getUsers = async (req, res) => {
  try {
    const users = await User.find();

    res.status(200).json(users);
  } catch (error) {
    res.status(500).json({
      message: "Failed to fetch users"
    });
  }
};

module.exports = {
  getUsers
};
```

Route:

```js
router.get("/", getUsers);
```

---

# 25. What is a service layer?

A service contains business logic.

Example:

```text
Route
  ↓
Controller
  ↓
Service
  ↓
Model
  ↓
Database
```

Controller:

```js
const createUser = async (req, res) => {
  const user = await userService.createUser(
    req.body
  );

  res.status(201).json(user);
};
```

Service:

```js
const createUser = async (data) => {
  return await User.create(data);
};
```

This separation makes larger applications easier to maintain and test.

---

# 26. What is error-handling middleware?

Express error-handling middleware uses four parameters:

```js
(err, req, res, next)
```

Example:

```js
app.use((err, req, res, next) => {
  console.error(err);

  res.status(500).json({
    message: "Internal Server Error"
  });
});
```

It should generally be registered after routes and other middleware.

---

# 27. Why use centralized error handling?

Without centralized handling, every controller may repeat:

```js
try {
  // ...
} catch (error) {
  res.status(500).json(...);
}
```

A centralized approach provides consistent:

* Error responses
* Logging
* Status codes
* Error handling

---

# 28. What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It controls which browser origins can access resources on your server.

Install:

```bash
npm install cors
```

Use:

```js
const cors = require("cors");

app.use(cors());
```

For production, configure allowed origins appropriately.

Example:

```js
app.use(
  cors({
    origin: "https://example.com"
  })
);
```

---

# 29. What is Helmet?

Helmet helps configure security-related HTTP response headers.

Install:

```bash
npm install helmet
```

Use:

```js
const helmet = require("helmet");

app.use(helmet());
```

It is one part of Express application security, not a complete security solution.

---

# 30. What is Morgan?

Morgan is an HTTP request logger.

Install:

```bash
npm install morgan
```

Use:

```js
const morgan = require("morgan");

app.use(morgan("dev"));
```

It can log information such as:

```text
HTTP method
URL
Status code
Response time
```

---

# 31. How do you handle 404 errors?

A catch-all route/middleware can handle requests that did not match an existing route.

Example:

```js
app.use((req, res) => {
  res.status(404).json({
    message: "Route not found"
  });
});
```

Place this after your defined routes.

---

# 32. How do you validate request data?

Validation ensures incoming data follows expected rules.

For example:

```js
if (!req.body.email) {
  return res.status(400).json({
    message: "Email is required"
  });
}
```

For larger applications, validation libraries such as:

```text
Zod
Joi
express-validator
```

can be used.

### Important Point

Never trust client-provided input.

---

# 33. What is authentication vs authorization?

### Authentication

Answers:

> Who are you?

Example:

```text
Login
 ↓
Verify email/password
 ↓
Generate token
```

### Authorization

Answers:

> What are you allowed to do?

Example:

```text
Admin → Delete product
User  → View product
```

---

# 34. How does JWT authentication work with Express?

Typical flow:

```text
Login Request
     ↓
Express Route
     ↓
Controller
     ↓
Find User
     ↓
Verify Password
     ↓
Create JWT
     ↓
Send Token
```

For protected routes:

```text
Request
   ↓
Authorization Header
   ↓
JWT Middleware
   ↓
Verify Token
   ↓
Attach User
   ↓
Controller
```

---

# 35. What is RESTful route organisation?

A clean API might look like:

```text
/api/auth
/api/users
/api/products
/api/orders
```

Example:

```text
POST   /api/auth/login
POST   /api/auth/register

GET    /api/products
GET    /api/products/:id
POST   /api/products
PATCH  /api/products/:id
DELETE /api/products/:id

GET    /api/orders
POST   /api/orders
GET    /api/orders/:id
```

---

# 36. What is a route handler?

A route handler is the function executed when a request matches a route.

```js
app.get("/users", (req, res) => {
  res.json({
    message: "Users fetched"
  });
});
```

The callback is the route handler.

---

# 37. Can a route have multiple middleware functions?

Yes.

```js
app.get(
  "/profile",
  authenticate,
  authorize,
  getProfile
);
```

Flow:

```text
Request
  ↓
authenticate
  ↓
authorize
  ↓
getProfile
  ↓
Response
```

---

# 38. What is middleware order and why is it important?

Express processes middleware in the order it is registered.

Example:

```js
app.use(express.json());

app.use("/api/users", userRoutes);

app.use(errorHandler);
```

If middleware is registered in the wrong order, requests may not behave as expected.

### Important Point

> Middleware order matters.

---

# 39. How do you structure a professional Express backend?

A common structure:

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

Flow:

```text
Client
  ↓
Routes
  ↓
Middleware
  ↓
Controller
  ↓
Service
  ↓
Model
  ↓
MongoDB
```

---

# 40. What is the difference between `app.use()` and `app.get()`?

### `app.use()`

Primarily registers middleware or mounts routers.

```js
app.use(express.json());

app.use("/api/users", userRoutes);
```

### `app.get()`

Handles a specific GET request.

```js
app.get("/users", getUsers);
```

---

# 41. What is `next()`?

`next()` passes control to the next middleware.

```js
const logger = (req, res, next) => {
  console.log(req.method);

  next();
};
```

Without calling `next()` or sending a response, the request can remain pending.

---

# 42. How do you send different response status codes?

```js
res.status(200).json({
  message: "Users fetched"
});
```

```js
res.status(201).json({
  message: "User created"
});
```

```js
res.status(400).json({
  message: "Invalid input"
});
```

```js
res.status(404).json({
  message: "User not found"
});
```

```js
res.status(500).json({
  message: "Internal server error"
});
```

---

# 43. How do you handle asynchronous errors?

Using `async/await`:

```js
const getUsers = async (req, res, next) => {
  try {
    const users = await User.find();

    res.json(users);
  } catch (error) {
    next(error);
  }
};
```

Then centralized error middleware handles the error:

```js
app.use((err, req, res, next) => {
  res.status(500).json({
    message: err.message
  });
});
```

---

# 44. What is API versioning?

API versioning allows you to evolve APIs without unexpectedly breaking existing clients.

Example:

```text
/api/v1/users
/api/v2/users
```

It can be useful when an API has multiple clients or significant contract changes.

---

# 45. What are important Express security practices?

Important practices include:

```text
Use HTTPS
Validate input
Configure CORS
Use Helmet
Rate-limit sensitive endpoints
Protect authentication routes
Hash passwords
Use secure cookies where appropriate
Keep secrets in environment variables
Avoid exposing stack traces in production
Keep dependencies updated
Implement authorization
```

---

# Express.js Interview Revision Checklist

## Core

* [ ] What is Express.js?
* [ ] Express vs Node.js
* [ ] Create Express application
* [ ] `app.listen()`
* [ ] Routing
* [ ] HTTP methods
* [ ] Route handlers

## Request & Response

* [ ] `req`
* [ ] `res`
* [ ] `req.params`
* [ ] `req.query`
* [ ] `req.body`
* [ ] `req.headers`
* [ ] `res.json()`
* [ ] `res.status()`

## Middleware

* [ ] Middleware
* [ ] `app.use()`
* [ ] `next()`
* [ ] Application middleware
* [ ] Router middleware
* [ ] Built-in middleware
* [ ] Third-party middleware
* [ ] Error middleware
* [ ] Middleware order

## Routing & Architecture

* [ ] `express.Router()`
* [ ] Routes
* [ ] Controllers
* [ ] Services
* [ ] Models
* [ ] REST API structure
* [ ] API versioning

## Security

* [ ] CORS
* [ ] Helmet
* [ ] Input validation
* [ ] Authentication
* [ ] Authorization
* [ ] JWT
* [ ] Rate limiting
* [ ] HTTPS
* [ ] Environment variables

## Errors

* [ ] 400
* [ ] 401
* [ ] 403
* [ ] 404
* [ ] 409
* [ ] 422
* [ ] 500
* [ ] Centralized error handling
* [ ] Async error handling

---

# Final Express.js Request Flow

Be able to explain this in an interview:

```text
Client
  ↓
HTTP Request
  ↓
Express Application
  ↓
Global Middleware
  ↓
Router
  ↓
Authentication Middleware
  ↓
Authorization Middleware
  ↓
Controller
  ↓
Service
  ↓
Model
  ↓
Database
  ↓
Controller
  ↓
HTTP Response
  ↓
Client
```

### One-Line Interview Answer

> **Express.js is a Node.js web framework that simplifies building HTTP servers and REST APIs through routing, middleware, request/response handling, and structured application architecture.**
