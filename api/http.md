# HTTP Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** HTTP fundamentals + commonly asked interview questions
> **Purpose:** Understand how clients and servers communicate over the web.

---

# 1. What is HTTP?

HTTP stands for **HyperText Transfer Protocol**.

It is a protocol used for communication between clients and servers.

Example:

```text
Frontend
   ↓
HTTP Request
   ↓
Backend Server
   ↓
HTTP Response
   ↓
Frontend
```

Example:

```text
GET /api/users
```

---

# 2. What is HTTPS?

HTTPS stands for **HyperText Transfer Protocol Secure**.

It is HTTP communication protected using TLS.

```text
HTTP
→ Data sent without TLS encryption

HTTPS
→ HTTP + TLS
```

HTTPS helps protect data from being read or modified while travelling between client and server.

---

# 3. HTTP vs HTTPS

| HTTP                         | HTTPS                        |
| ---------------------------- | ---------------------------- |
| No TLS protection            | Uses TLS                     |
| Less secure                  | More secure                  |
| Usually port 80              | Usually port 443             |
| Data is not protected by TLS | Data is protected in transit |

For production web applications, HTTPS should normally be used.

---

# 4. What is a client?

A client is a system that sends requests to a server.

Examples:

```text
Browser
React Application
Mobile Application
Postman
Flutter Application
```

Example:

```text
React App
   ↓
GET /api/products
```

---

# 5. What is a server?

A server receives client requests, processes them, and sends responses.

Example:

```text
Client
   ↓
Express Server
   ↓
MongoDB
   ↓
Response
```

---

# 6. What is an HTTP request?

An HTTP request is a message sent by a client to a server.

A request can contain:

```text
Method
URL
Headers
Body
```

Example:

```http
POST /api/users HTTP/1.1
Content-Type: application/json
```

```json
{
  "name": "Veera",
  "email": "veera@example.com"
}
```

---

# 7. What is an HTTP response?

An HTTP response is the message sent by the server back to the client.

It commonly contains:

```text
Status Code
Headers
Body
```

Example:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "message": "User fetched successfully"
}
```

---

# 8. What is an HTTP method?

HTTP methods describe the intended operation of a request.

Common methods:

```text
GET
POST
PUT
PATCH
DELETE
```

Simple meaning:

```text
GET     → Read
POST    → Create
PUT     → Replace
PATCH   → Partially update
DELETE  → Delete
```

---

# 9. What is GET?

`GET` is commonly used to retrieve data.

Example:

```http
GET /api/users
```

Response:

```json
[
  {
    "id": 1,
    "name": "Veera"
  }
]
```

GET requests should generally not be used to modify server state.

---

# 10. What is POST?

`POST` is commonly used to create a resource or submit data for processing.

Example:

```http
POST /api/users
```

Body:

```json
{
  "name": "Veera",
  "email": "veera@example.com"
}
```

---

# 11. What is PUT?

`PUT` is commonly used to replace a resource with a new representation.

Example:

```http
PUT /api/users/101
```

```json
{
  "name": "Veera",
  "email": "new@example.com"
}
```

---

# 12. What is PATCH?

`PATCH` is commonly used for a partial update.

Example:

```http
PATCH /api/users/101
```

```json
{
  "name": "Veerababu"
}
```

Only the specified field needs to be changed.

---

# 13. What is DELETE?

`DELETE` is used to request deletion of a resource.

Example:

```http
DELETE /api/users/101
```

---

# 14. PUT vs PATCH

| PUT                                        | PATCH                               |
| ------------------------------------------ | ----------------------------------- |
| Commonly represents full replacement       | Commonly represents partial update  |
| Client generally sends full representation | Client can send only changed fields |
| Used for replacement semantics             | Used for partial modification       |

Example:

```text
PUT
→ Replace complete user

PATCH
→ Change only email
```

---

# 15. What are HTTP status codes?

Status codes tell the client the result of a request.

They are grouped into categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client error
5xx → Server error
```

---

# 16. What is 200 OK?

`200 OK` means the request was successfully processed.

Example:

```http
HTTP/1.1 200 OK
```

Commonly used for successful GET requests.

---

# 17. What is 201 Created?

`201 Created` means a new resource was successfully created.

Example:

```http
POST /api/users
```

Response:

```http
HTTP/1.1 201 Created
```

---

# 18. What is 204 No Content?

`204 No Content` means the request succeeded but there is no response body to return.

Example:

```text
DELETE /api/users/101
→ 204 No Content
```

---

# 19. What is 400 Bad Request?

`400` indicates that the server could not process the request because the request was invalid.

Example:

```json
{
  "email": "not-valid"
}
```

The API may return:

```http
400 Bad Request
```

---

# 20. What is 401 Unauthorized?

`401` indicates that valid authentication credentials are missing or invalid.

Example:

```text
No JWT
   ↓
Protected API
   ↓
401 Unauthorized
```

---

# 21. What is 403 Forbidden?

`403` means the server understood the request but refuses to allow the operation.

Example:

```text
Authenticated User
       ↓
Tries Admin Operation
       ↓
Not enough permission
       ↓
403 Forbidden
```

### Important

```text
401 → Authentication problem

403 → Authorization/permission problem
```

---

# 22. What is 404 Not Found?

`404` means the requested resource or route could not be found.

Example:

```http
GET /api/users/999999
```

If the user does not exist:

```http
404 Not Found
```

---

# 23. What is 409 Conflict?

`409 Conflict` indicates that the request conflicts with the current state of the resource.

Example:

```text
Register with an email that already exists
```

Response:

```http
409 Conflict
```

---

# 24. What is 422 Unprocessable Content?

`422` is commonly used when the request format is understood but the supplied data fails validation or semantic rules.

Example:

```json
{
  "age": -5
}
```

The server understands the request but rejects the invalid value.

---

# 25. What is 500 Internal Server Error?

`500` means the server encountered an unexpected condition while processing the request.

Example:

```text
Database failure
Unexpected server error
Unhandled application error
```

---

# 26. What are HTTP headers?

Headers contain metadata about a request or response.

Request headers:

```text
Authorization
Content-Type
Accept
User-Agent
```

Response headers:

```text
Content-Type
Cache-Control
Set-Cookie
```

---

# 27. What is Content-Type?

`Content-Type` tells the receiver what type of data is contained in the request or response body.

Example:

```http
Content-Type: application/json
```

This means the body contains JSON.

Other examples:

```text
text/html
text/plain
multipart/form-data
application/x-www-form-urlencoded
```

---

# 28. What is Accept?

`Accept` tells the server which response media types the client can handle.

Example:

```http
Accept: application/json
```

The client is indicating that it expects JSON.

---

# 29. What is Authorization header?

The `Authorization` header is commonly used to send authentication credentials.

JWT example:

```http
Authorization: Bearer eyJhbGciOi...
```

Typical flow:

```text
Client
   ↓
Authorization: Bearer <JWT>
   ↓
Server
   ↓
Verify Token
```

---

# 30. What is a URL?

URL stands for **Uniform Resource Locator**.

Example:

```text
https://example.com/api/users/101
```

It can contain:

```text
Protocol
Domain
Path
Query parameters
```

Example:

```text
https://example.com/products?page=2
```

Here:

```text
Domain → example.com
Path   → /products
Query  → page=2
```

---

# 31. What are query parameters?

Query parameters provide additional information in a URL.

Example:

```text
GET /api/products?page=2&limit=10
```

Parameters:

```text
page = 2
limit = 10
```

They are commonly used for:

```text
Filtering
Searching
Sorting
Pagination
```

---

# 32. What are path parameters?

Path parameters identify a specific resource.

Example:

```text
GET /api/users/101
```

Here:

```text
101
```

is the user ID.

In Express:

```js
app.get("/api/users/:id", (req, res) => {
  console.log(req.params.id);
});
```

---

# 33. Query parameter vs path parameter

| Path Parameter        | Query Parameter            |
| --------------------- | -------------------------- |
| Identifies a resource | Modifies/refines a request |
| `/users/101`          | `/users?page=2`            |
| `req.params`          | `req.query`                |

Simple rule:

```text
/users/101
→ Which user?

/users?page=2
→ Which page?
```

---

# 34. What is the HTTP request-response cycle?

```text
Client
  ↓
HTTP Request
  ↓
Server
  ↓
Route
  ↓
Middleware
  ↓
Controller
  ↓
Database
  ↓
Controller
  ↓
HTTP Response
  ↓
Client
```

This is one of the most important concepts for backend interviews.

---

# 35. Is HTTP stateful or stateless?

HTTP itself is generally considered **stateless**.

Each request is treated independently at the protocol level.

Example:

```text
Request 1
GET /products

Request 2
GET /orders
```

The server does not inherently remember the previous request simply because HTTP was used.

Applications can add state using:

```text
Cookies
Sessions
Tokens
Databases
```

---

# 36. What are cookies?

Cookies are small pieces of data stored by the browser and sent with matching requests.

Common uses:

```text
Authentication
Session identifiers
Preferences
Tracking
```

A secure authentication cookie may use:

```text
HttpOnly
Secure
SameSite
```

---

# 37. What is a session?

A session allows the server to maintain state associated with a client.

Typical flow:

```text
Login
 ↓
Server creates session
 ↓
Session ID sent to browser
 ↓
Browser sends session ID
 ↓
Server finds session
 ↓
User identified
```

---

# 38. HTTP cookies vs sessions

```text
Cookie
→ Data stored on the client/browser.

Session
→ Authentication/state maintained by the server,
   usually identified by a session ID.
```

A session ID is often stored in a cookie.

---

# 39. What is caching?

Caching stores reusable data so future requests can be served more efficiently.

Example:

```text
Client
 ↓
Request
 ↓
Cache
 ↓
Cached Response
```

HTTP caching uses headers such as:

```text
Cache-Control
ETag
Last-Modified
```

---

# 40. What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It controls whether a browser allows a web page from one origin to access resources from another origin.

Example:

```text
Frontend
http://localhost:3000

Backend
http://localhost:5000
```

These are different origins.

The backend can configure CORS to allow the required frontend origin.

---

# 41. What is an HTTP origin?

An origin is determined by:

```text
Scheme
Host
Port
```

Example:

```text
http://localhost:3000
```

If any of these differ, the origin is different.

```text
http://localhost:3000
http://localhost:5000
```

Different ports mean different origins.

---

# 42. What is idempotency?

An operation is idempotent if repeating the same request has the same intended final effect as making it once.

Commonly considered idempotent:

```text
GET
PUT
DELETE
```

`POST` is generally not considered idempotent by default.

### Example

```text
PUT /users/101
```

Sending the same replacement multiple times should result in the same final resource representation.

---

# 43. What is safe HTTP method?

A safe method is intended only to retrieve information and not change server state.

Common safe methods:

```text
GET
HEAD
OPTIONS
```

---

# 44. What is HTTP persistent connection?

HTTP can reuse a TCP connection for multiple requests instead of creating a new connection for every request.

This reduces connection overhead.

Modern HTTP versions also provide more advanced transport behaviour.

---

# 45. What is HTTP/1.1?

HTTP/1.1 is a widely used HTTP version that introduced or standardised features such as:

```text
Persistent connections
Host header
Chunked transfer encoding
Better caching controls
```

---

# 46. What is HTTP/2?

HTTP/2 improves HTTP communication efficiency.

Important features include:

```text
Binary framing
Multiplexing
Header compression
Stream prioritisation mechanisms
```

A major benefit is that multiple streams can share a connection.

---

# 47. What is HTTP/3?

HTTP/3 uses **QUIC** as its transport protocol instead of TCP.

Important characteristics include:

```text
QUIC
UDP-based transport
Multiplexed streams
TLS 1.3 integration
```

It is designed to improve performance and connection behaviour, especially under changing network conditions.

---

# 48. What is REST?

REST stands for **Representational State Transfer**.

It is an architectural style for designing networked applications.

REST commonly uses:

```text
Resources
HTTP methods
HTTP status codes
Representations such as JSON
Stateless requests
```

---

# 49. What is an HTTP request body?

The request body contains data sent to the server.

Example:

```http
POST /api/users
Content-Type: application/json
```

```json
{
  "name": "Veera",
  "email": "veera@example.com"
}
```

---

# 50. What is the difference between request headers and request body?

```text
Headers
→ Metadata about the request.

Body
→ Actual data being submitted.
```

Example:

```text
Authorization header
→ Authentication information

JSON body
→ User information
```

---

# HTTP Revision Checklist

* [ ] HTTP
* [ ] HTTPS
* [ ] Client
* [ ] Server
* [ ] Request
* [ ] Response
* [ ] HTTP methods
* [ ] Status codes
* [ ] Headers
* [ ] Content-Type
* [ ] Authorization
* [ ] URL
* [ ] Query parameters
* [ ] Path parameters
* [ ] Cookies
* [ ] Sessions
* [ ] CORS
* [ ] Origin
* [ ] Caching
* [ ] Idempotency
* [ ] Safe methods
* [ ] HTTP/1.1
* [ ] HTTP/2
* [ ] HTTP/3
* [ ] Request-response lifecycle

---

# Final HTTP Flow

```text
Client
   ↓
HTTP Request
   │
   ├── Method
   ├── URL
   ├── Headers
   └── Body
   ↓
Server
   ↓
Process Request
   ↓
HTTP Response
   │
   ├── Status Code
   ├── Headers
   └── Body
   ↓
Client
```

### One-Line Interview Answer

> **HTTP is a protocol that defines how clients and servers communicate through requests and responses over a network.**
