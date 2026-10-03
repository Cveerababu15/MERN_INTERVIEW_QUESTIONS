# Postman Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** API testing and debugging using Postman
> **Goal:** Understand how to test REST APIs before connecting the frontend.

---

# 1. What is Postman?

Postman is a tool used to develop, test, and debug APIs.

It allows you to send HTTP requests such as:

```text
GET
POST
PUT
PATCH
DELETE
```

and inspect the server response.

Typical workflow:

```text
Postman
   ↓
REST API
   ↓
Express
   ↓
Database
   ↓
Response
```

---

# 2. Why do developers use Postman?

Postman helps test the backend independently from the frontend.

You can test:

* API routes
* Request bodies
* Query parameters
* Headers
* Authentication
* Status codes
* Response data
* Error cases

This is especially useful while developing a MERN backend.

---

# 3. How do you send a GET request?

Select:

```text
GET
```

Enter:

```text
http://localhost:5000/api/users
```

Then click:

```text
Send
```

Postman displays the server response.

---

# 4. How do you send a POST request?

Select:

```text
POST
```

URL:

```text
http://localhost:5000/api/users
```

Choose:

```text
Body
→ raw
→ JSON
```

Example:

```json
{
  "name": "Veera",
  "email": "veera@example.com",
  "password": "password123"
}
```

Then click **Send**.

---

# 5. How do you send a PUT or PATCH request?

Example:

```text
PATCH
http://localhost:5000/api/users/101
```

Body:

```json
{
  "name": "Veerababu"
}
```

This allows you to test update endpoints.

---

# 6. How do you send a DELETE request?

Select:

```text
DELETE
```

Example:

```text
http://localhost:5000/api/users/101
```

Click:

```text
Send
```

Then inspect the response status and body.

---

# 7. What are request headers?

Headers provide metadata about the request.

Example:

```text
Content-Type: application/json
```

Authentication:

```text
Authorization: Bearer <JWT>
```

In Postman:

```text
Headers
→ Key
→ Value
```

---

# 8. How do you send JSON data?

Go to:

```text
Body
→ raw
→ JSON
```

Example:

```json
{
  "name": "Veera",
  "age": 21
}
```

Postman generally sets:

```text
Content-Type: application/json
```

when JSON mode is selected.

---

# 9. What are query parameters in Postman?

Example API:

```text
GET /api/products?page=2&limit=10
```

In Postman, use the **Params** section:

```text
KEY      VALUE
page     2
limit    10
```

Postman builds the query string.

---

# 10. What is path parameter testing?

Example:

```text
GET /api/products/101
```

Here:

```text
101
```

is the path parameter.

You can replace it with another ID:

```text
GET /api/products/102
```

---

# 11. How do you test JWT authentication in Postman?

First call:

```text
POST /api/auth/login
```

Example response:

```json
{
  "token": "eyJhbGciOi..."
}
```

Then call a protected endpoint.

Header:

```text
Authorization: Bearer <token>
```

Flow:

```text
Login
 ↓
Get JWT
 ↓
Send JWT
 ↓
Protected API
 ↓
Response
```

---

# 12. What is the Authorization tab?

Postman provides an **Authorization** section where you can configure authentication for a request.

For JWT:

```text
Type → Bearer Token
Token → <JWT>
```

Postman then sends the appropriate authorization header.

---

# 13. What is a Postman Collection?

A collection groups related API requests.

Example:

```text
Restaurant API
├── Authentication
│   ├── Register
│   └── Login
│
├── Restaurants
│   ├── Get Restaurants
│   ├── Create Restaurant
│   └── Update Restaurant
│
└── Orders
    ├── Create Order
    └── Get Orders
```

Collections keep API testing organised.

---

# 14. What is a Postman Environment?

An environment stores reusable variables.

Example:

```text
BASE_URL
TOKEN
USER_ID
```

Example:

```text
BASE_URL = http://localhost:5000
```

Then use:

```text
{{BASE_URL}}/api/users
```

This is useful when switching between:

```text
Development
Testing
Production
```

---

# 15. What are Postman variables?

Variables allow reusable values.

Example:

```text
{{baseUrl}}
{{token}}
{{userId}}
```

Instead of repeatedly writing:

```text
http://localhost:5000
```

you can use:

```text
{{baseUrl}}
```

---

# 16. How do you test API error cases?

Do not test only successful requests.

Also test:

```text
Missing fields
Invalid ID
Invalid token
Expired token
Duplicate email
Unauthorized access
Invalid JSON
Non-existent resource
```

Example:

```text
POST /api/users
```

with:

```json
{
  "name": ""
}
```

Expected response might be:

```text
400
```

depending on the API contract.

---

# 17. What should you check after sending a request?

Check:

```text
Status code
Response body
Response headers
Response time
Error message
```

Example:

```text
201 Created
```

means the resource was successfully created.

---

# 18. What is API testing flow using Postman?

```text
Create API
    ↓
Start Backend
    ↓
Open Postman
    ↓
Send Request
    ↓
Check Status Code
    ↓
Check Response
    ↓
Test Error Cases
    ↓
Fix Backend
    ↓
Test Again
```

---

# 19. Why test backend APIs before connecting React?

Because it separates backend problems from frontend problems.

Example:

```text
Postman
   ↓
API works
   ↓
Connect React
```

If the API does not work in Postman, frontend debugging can create unnecessary confusion.

---

# 20. What are Postman tests?

Postman can run JavaScript-based test scripts against responses.

Conceptually:

```javascript
pm.test("Status is 200", function () {
  pm.response.to.have.status(200);
});
```

Tests can verify expected API behaviour.

---

# Postman Revision Checklist

* [ ] What is Postman?
* [ ] GET request
* [ ] POST request
* [ ] PUT request
* [ ] PATCH request
* [ ] DELETE request
* [ ] Headers
* [ ] JSON body
* [ ] Query parameters
* [ ] Path parameters
* [ ] JWT authentication
* [ ] Authorization
* [ ] Collections
* [ ] Environments
* [ ] Variables
* [ ] Error testing
* [ ] Response validation
* [ ] Postman tests

---

# Final Postman Flow

```text
Postman
   ↓
Request
   ├── Method
   ├── URL
   ├── Headers
   ├── Params
   └── Body
   ↓
Backend API
   ↓
Response
   ├── Status
   ├── Headers
   └── Body
```

### One-Line Interview Answer

> **Postman is an API development and testing tool used to send HTTP requests and inspect, validate, and debug API responses.**
