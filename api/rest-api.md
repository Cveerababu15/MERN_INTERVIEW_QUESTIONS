# REST API Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** REST API fundamentals + commonly asked interview questions
> **Prerequisite:** HTTP + Node.js + Express.js

---

# 1. What is an API?

API stands for **Application Programming Interface**.

It provides a way for different software systems to communicate.

Example:

```text
React Application
      ↓
      API
      ↓
Node.js Backend
      ↓
   MongoDB
```

The frontend does not directly need to access the database.

---

# 2. What is a REST API?

A REST API is an API designed according to the principles of **REST — Representational State Transfer**.

REST APIs commonly use:

```text
HTTP
Resources
HTTP methods
Status codes
JSON
Stateless requests
```

Example:

```text
GET    /api/products
POST   /api/products
GET    /api/products/101
PATCH  /api/products/101
DELETE /api/products/101
```

---

# 3. What is a resource in REST?

A resource is an entity that the API exposes.

Examples:

```text
users
products
orders
restaurants
branches
payments
```

Example:

```text
/api/users
/api/products
/api/orders
```

---

# 4. Why are REST APIs commonly used?

REST APIs are popular because they:

* Use standard HTTP
* Are easy to understand
* Work with many clients
* Separate frontend and backend
* Support scalable application architectures
* Commonly use JSON
* Fit naturally with web applications

Example:

```text
React
Flutter
Mobile App
Postman
     ↓
   REST API
     ↓
Backend
```

---

# 5. What are the main REST principles?

Common REST constraints include:

```text
Client-Server
Statelessness
Cacheability
Uniform Interface
Layered System
Code on Demand (optional)
```

The most commonly discussed in interviews are:

```text
Stateless
Client-Server
Resource-based design
Uniform interface
Cacheability
Layered architecture
```

---

# 6. What is statelessness in REST?

Each request should contain the information necessary for the server to process it.

The server should not depend on previous requests being stored as conversational state.

Example:

```text
Request 1
GET /api/products

Request 2
GET /api/orders
Authorization: Bearer <token>
```

Each protected request contains its authentication information.

---

# 7. What is client-server architecture?

REST separates the client and server responsibilities.

```text
Client
→ UI / user interaction

Server
→ Business logic / data access
```

Example:

```text
React
   ↓
REST API
   ↓
Express
   ↓
MongoDB
```

The frontend and backend can evolve independently as long as their API contract remains compatible.

---

# 8. What is a REST resource URL?

A resource should generally be represented using a noun.

Good:

```text
/api/users
/api/products
/api/orders
```

Less REST-oriented:

```text
/api/getUsers
/api/createProduct
/api/deleteOrder
```

The HTTP method describes the operation.

---

# 9. What are HTTP methods used in REST?

```text
GET
POST
PUT
PATCH
DELETE
```

Typical mapping:

```text
GET
→ Read

POST
→ Create

PUT
→ Replace

PATCH
→ Partial update

DELETE
→ Delete
```

---

# 10. How do you design CRUD REST endpoints?

For a `products` resource:

```text
GET    /api/products
POST   /api/products

GET    /api/products/:id
PUT    /api/products/:id
PATCH  /api/products/:id
DELETE /api/products/:id
```

Example:

```text
GET /api/products
```

Fetch all products.

```text
POST /api/products
```

Create a product.

---

# 11. What is the difference between GET and POST?

| GET                                     | POST                                                |
| --------------------------------------- | --------------------------------------------------- |
| Retrieves data                          | Submits data                                        |
| Usually no request body                 | Commonly has a body                                 |
| Safe                                    | Not safe                                            |
| Generally idempotent                    | Generally not idempotent                            |
| Can be cached under suitable conditions | Usually not treated as a simple cacheable retrieval |

Example:

```text
GET /api/products
```

```text
POST /api/products
```

---

# 12. PUT vs PATCH in REST

```text
PUT
→ Full replacement semantics

PATCH
→ Partial modification semantics
```

Example:

```http
PUT /api/users/101
```

```json
{
  "name": "Veera",
  "email": "veera@example.com",
  "phone": "9999999999"
}
```

PATCH:

```http
PATCH /api/users/101
```

```json
{
  "phone": "8888888888"
}
```

---

# 13. What is a REST endpoint?

An endpoint is a specific API location through which a client interacts with a resource.

Example:

```text
GET /api/users
```

The combination of HTTP method and URL identifies the operation.

```text
GET + /api/users
```

is different from:

```text
POST + /api/users
```

---

# 14. What is an API route?

An API route defines how the backend responds to a particular HTTP method and path.

Express example:

```js
router.get("/products", getProducts);

router.post("/products", createProduct);

router.delete(
  "/products/:id",
  deleteProduct
);
```

---

# 15. What is JSON?

JSON stands for **JavaScript Object Notation**.

It is a common data format used for API communication.

Example:

```json
{
  "id": 101,
  "name": "Laptop",
  "price": 50000
}
```

JSON is language-independent despite its JavaScript-inspired syntax.

---

# 16. What should a REST API response contain?

A response commonly contains:

```text
Status Code
Headers
Body
```

Example:

```json
{
  "success": true,
  "message": "Product fetched successfully",
  "data": {
    "id": 101,
    "name": "Laptop"
  }
}
```

---

# 17. What HTTP status codes are important for REST APIs?

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

---

# 18. What is API versioning?

API versioning allows an API to evolve while supporting existing clients.

Example:

```text
/api/v1/users
/api/v2/users
```

Versioning is useful when a breaking API contract change is introduced.

---

# 19. What are common API versioning strategies?

Common approaches include:

### URL Versioning

```text
/api/v1/users
/api/v2/users
```

### Header Versioning

```http
Accept: application/vnd.example.v2+json
```

### Query Parameter

```text
/api/users?version=2
```

The URL-based approach is simple and commonly understood.

---

# 20. What is API authentication?

Authentication verifies the identity of the client/user.

Common approaches:

```text
Session-based authentication
JWT
OAuth 2.0
API keys
```

Example JWT request:

```http
GET /api/profile
Authorization: Bearer <token>
```

---

# 21. What is API authorization?

Authorization determines whether an authenticated user can perform a specific operation.

Example:

```text
User
→ View products

Admin
→ Create products
→ Update products
→ Delete products
```

---

# 22. Authentication vs authorization in REST APIs

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

Typical request:

```text
Client
 ↓
JWT
 ↓
Authentication
 ↓
Authorization
 ↓
Controller
```

---

# 23. How do you protect a REST API?

Common measures include:

```text
Authentication
Authorization
Input validation
HTTPS
Rate limiting
Secure headers
CORS configuration
Access control
Secure secret management
Logging and monitoring
```

Example:

```text
Request
   ↓
JWT Middleware
   ↓
RBAC Middleware
   ↓
Controller
```

---

# 24. What is pagination?

Pagination divides a large result set into smaller pages.

Example:

```text
GET /api/products?page=2&limit=20
```

Response:

```json
{
  "data": [],
  "page": 2,
  "limit": 20,
  "total": 150
}
```

Benefits:

```text
Less data transferred
Faster responses
Better UI performance
Lower server/database workload
```

---

# 25. What is filtering?

Filtering returns only resources matching specified conditions.

Example:

```text
GET /api/products?category=electronics
```

Multiple filters:

```text
GET /api/products?category=electronics&brand=Apple
```

---

# 26. What is sorting?

Sorting controls the order of returned resources.

Example:

```text
GET /api/products?sort=price
```

Descending:

```text
GET /api/products?sort=-price
```

The exact API syntax is application-specific.

---

# 27. What is searching in a REST API?

Search allows clients to find resources based on text or other criteria.

Example:

```text
GET /api/products?search=laptop
```

The backend can translate the search criteria into a database query.

---

# 28. What is nested routing?

Nested routes represent a relationship between resources.

Example:

```text
GET /api/users/101/orders
```

Meaning:

```text
Orders belonging to user 101
```

Another example:

```text
GET /api/restaurants/10/branches
```

---

# 29. When should nested routes be used?

Nested routes are useful when the child resource strongly depends on the parent context.

Example:

```text
/users/:userId/orders
```

However, deeply nested URLs can become difficult to maintain.

Avoid unnecessarily deep structures such as:

```text
/api/users/1/orders/10/items/5/reviews/2
```

Keep API design understandable.

---

# 30. What is HATEOAS?

HATEOAS stands for:

**Hypermedia As The Engine Of Application State**

The server includes links or actions in responses that help clients discover related operations.

Conceptually:

```json
{
  "id": 101,
  "name": "Laptop",
  "links": {
    "self": "/api/products/101",
    "reviews": "/api/products/101/reviews"
  }
}
```

It is part of the broader REST architectural constraints, although many practical REST APIs do not fully implement HATEOAS.

---

# 31. What is idempotency in REST?

An operation is idempotent when repeating the same request has the same intended final effect as making it once.

Common examples:

```text
GET
PUT
DELETE
```

Example:

```text
DELETE /api/users/101
```

After the user is deleted, repeating the request should not recreate or modify the resource.

The exact response status can still differ.

---

# 32. What is a safe method?

A safe HTTP method is intended for retrieving information rather than modifying server state.

Examples:

```text
GET
HEAD
OPTIONS
```

In REST API design, avoid using GET for operations that change data.

Bad:

```text
GET /api/deleteUser/101
```

Better:

```text
DELETE /api/users/101
```

---

# 33. What is API validation?

API validation checks whether incoming data is valid before processing it.

Example:

```json
{
  "email": "invalid"
}
```

Backend:

```text
Request
 ↓
Validation
 ↓
Invalid
 ↓
400 / 422
```

Validation should happen on the server even if the frontend also validates.

---

# 34. What is API error handling?

A REST API should return consistent error responses.

Example:

```json
{
  "success": false,
  "message": "Product not found"
}
```

With:

```http
404 Not Found
```

A common structure:

```text
Request
 ↓
Controller
 ↓
Error
 ↓
Central Error Handler
 ↓
HTTP Status
 ↓
JSON Response
```

---

# 35. What is rate limiting?

Rate limiting controls how many requests a client can make within a period.

Example:

```text
100 requests / minute
```

If the limit is exceeded, the server can reject additional requests.

Useful for:

```text
Login
OTP
Password reset
Public APIs
Expensive endpoints
```

---

# 36. What is CORS in REST APIs?

CORS controls browser access to resources from different origins.

Example:

```text
Frontend
http://localhost:3000

Backend
http://localhost:5000
```

Express:

```js
const cors = require("cors");

app.use(
  cors({
    origin: "http://localhost:3000"
  })
);
```

---

# 37. What is content negotiation?

Content negotiation allows the client and server to agree on the representation format.

Client:

```http
Accept: application/json
```

Server:

```http
Content-Type: application/json
```

JSON is the most common format for modern REST APIs.

---

# 38. What is an API contract?

An API contract defines how clients and servers communicate.

It can describe:

```text
Endpoint
HTTP method
Parameters
Request body
Response body
Status codes
Authentication
Validation rules
```

Example:

```text
POST /api/users

Request:
{
  "name": "Veera",
  "email": "veera@example.com"
}

Response:
201 Created
{
  "id": 101,
  "name": "Veera"
}
```

---

# 39. What is OpenAPI / Swagger?

OpenAPI is a specification for describing HTTP APIs.

Swagger tools can be used to:

```text
Document APIs
Explore endpoints
Generate documentation
Test APIs
Generate client/server code in supported workflows
```

Example documentation can describe:

```text
GET /api/products
POST /api/products
GET /api/products/{id}
```

---

# 40. What is Postman?

Postman is a tool commonly used to test APIs.

You can send:

```text
GET
POST
PUT
PATCH
DELETE
```

and inspect:

```text
Status code
Headers
Response body
Response time
```

Example:

```text
Postman
   ↓
POST /api/login
   ↓
Express API
   ↓
JSON Response
```

---

# 41. REST API vs GraphQL

| REST                                            | GraphQL                                 |
| ----------------------------------------------- | --------------------------------------- |
| Multiple resource endpoints                     | Commonly a single endpoint              |
| Server defines response structures per endpoint | Client specifies requested fields       |
| Uses HTTP methods heavily                       | Usually uses POST for queries/mutations |
| Simple to understand                            | Flexible data fetching                  |
| Easy HTTP caching patterns                      | Caching can require additional design   |

Both can be valid depending on the application.

---

# 42. REST API vs SOAP

| REST                             | SOAP                                 |
| -------------------------------- | ------------------------------------ |
| Architectural style              | Protocol                             |
| Commonly uses JSON               | Commonly XML                         |
| Lightweight in many web APIs     | More formal messaging standards      |
| Uses HTTP commonly               | Can use multiple transport protocols |
| Common in modern web/mobile APIs | Common in some enterprise systems    |

---

# 43. What is a stateless REST API flow?

```text
Client
  ↓
Request + Required Information
  ↓
REST API
  ↓
Authentication
  ↓
Business Logic
  ↓
Database
  ↓
Response
```

The server does not need to depend on application-level session state from previous requests to understand the current request.

---

# 44. What is a good REST API naming convention?

Prefer plural nouns:

```text
/api/users
/api/products
/api/orders
```

Use IDs for individual resources:

```text
/api/users/101
/api/products/50
/api/orders/900
```

Avoid action-based URLs when an HTTP method can express the operation:

```text
Avoid:
POST /api/createUser

Prefer:
POST /api/users
```

---

# 45. What is a REST API request lifecycle in Express?

Example:

```text
React / Flutter
      ↓
HTTP Request
      ↓
Express
      ↓
CORS / JSON Middleware
      ↓
Router
      ↓
Authentication
      ↓
Authorization
      ↓
Controller
      ↓
Service
      ↓
Model
      ↓
MongoDB
      ↓
Service
      ↓
Controller
      ↓
JSON Response
      ↓
Client
```

---

# 46. Example REST API structure

A professional Express project can be organised as:

```text
src/
├── config/
├── controllers/
├── middleware/
├── models/
├── routes/
├── services/
├── utils/
├── app.js
└── server.js
```

Example:

```text
routes/productRoutes.js
        ↓
controllers/productController.js
        ↓
services/productService.js
        ↓
models/Product.js
        ↓
MongoDB
```

---

# 47. Example REST API

### Route

```js
router.get(
  "/products",
  getProducts
);
```

### Controller

```js
const getProducts = async (req, res, next) => {
  try {
    const products =
      await productService.getProducts();

    res.status(200).json({
      success: true,
      data: products
    });
  } catch (error) {
    next(error);
  }
};
```

### Request

```http
GET /api/products
```

### Response

```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Laptop"
    }
  ]
}
```

---

# 48. How does JWT work in a REST API?

Typical flow:

```text
POST /api/auth/login
        ↓
Verify credentials
        ↓
Generate JWT
        ↓
Client receives token
        ↓
Client sends token
        ↓
Authorization: Bearer <token>
        ↓
Authentication middleware
        ↓
Verify JWT
        ↓
Protected API
```

Example:

```http
GET /api/profile
Authorization: Bearer <JWT>
```

---

# 49. What is the difference between REST API and API?

```text
API
→ General concept for communication between software components.

REST API
→ An API designed using REST architectural principles,
   commonly using HTTP.
```

So:

```text
Every REST API is an API.

Not every API is a REST API.
```

---

# 50. What makes a REST API well designed?

Important characteristics include:

```text
Clear resource naming
Correct HTTP methods
Meaningful status codes
Consistent response format
Validation
Authentication
Authorization
Pagination
Filtering
Sorting
Error handling
API documentation
Versioning when required
Security
```

---

# REST API Revision Checklist

## Fundamentals

* [ ] API
* [ ] REST
* [ ] REST API
* [ ] Resource
* [ ] Endpoint
* [ ] Statelessness
* [ ] Client-server architecture
* [ ] REST constraints

## HTTP

* [ ] GET
* [ ] POST
* [ ] PUT
* [ ] PATCH
* [ ] DELETE
* [ ] Status codes
* [ ] Headers
* [ ] Request body
* [ ] Response body

## API Design

* [ ] Resource naming
* [ ] CRUD endpoints
* [ ] Path parameters
* [ ] Query parameters
* [ ] Nested routes
* [ ] API versioning
* [ ] Pagination
* [ ] Filtering
* [ ] Sorting
* [ ] Searching

## Security

* [ ] Authentication
* [ ] Authorization
* [ ] JWT
* [ ] RBAC
* [ ] HTTPS
* [ ] CORS
* [ ] Rate limiting
* [ ] Input validation

## Advanced

* [ ] Idempotency
* [ ] Safe methods
* [ ] Caching
* [ ] Content negotiation
* [ ] HATEOAS
* [ ] OpenAPI
* [ ] API contracts

## Tools

* [ ] Postman
* [ ] Swagger
* [ ] API testing

---

# Final REST API Flow

```text
                    CLIENT
                       ↓
                HTTP Request
                       ↓
                REST Endpoint
                       ↓
                  Middleware
                       ↓
              Authentication
                       ↓
               Authorization
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
                JSON Response
                       ↓
                    CLIENT
```

---

# Quick REST API Example

```text
Resource: Products

GET    /api/products
       → Get all products

POST   /api/products
       → Create product

GET    /api/products/101
       → Get product 101

PUT    /api/products/101
       → Replace product 101

PATCH  /api/products/101
       → Update part of product 101

DELETE /api/products/101
       → Delete product 101
```

---

# Final Interview Questions You Must Be Able to Answer

```text
1. What is REST?

2. What is a REST API?

3. What is a resource?

4. What is an endpoint?

5. Why are nouns used in REST URLs?

6. GET vs POST?

7. PUT vs PATCH?

8. What does stateless mean?

9. What are HTTP status codes?

10. What is API versioning?

11. What is pagination?

12. What is authentication?

13. What is authorization?

14. How does JWT work with REST APIs?

15. What is CORS?

16. What is rate limiting?

17. What is idempotency?

18. What is API validation?

19. How do you handle API errors?

20. How does a REST request travel through an Express backend?
```

### One-Line Interview Answer

> **A REST API is an HTTP-based API that exposes resources through well-defined endpoints and uses standard HTTP methods, status codes, and stateless communication to allow clients and servers to interact.**
