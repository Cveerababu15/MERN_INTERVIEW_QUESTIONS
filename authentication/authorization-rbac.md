# RBAC Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** Role-Based Access Control + authentication/authorization interview questions
> **Prerequisite:** Node.js + Express.js + MongoDB + JWT

---

# 1. What is Authorization?

Authorization determines **what an authenticated user is allowed to do**.

Example:

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

# 2. What is RBAC?

RBAC stands for **Role-Based Access Control**.

It controls access to resources based on the user's role.

Example:

```text
Admin
 ├── Create Product
 ├── Update Product
 ├── Delete Product
 └── View Orders

Manager
 ├── Update Product
 └── View Orders

User
 ├── View Products
 └── Create Orders
```

---

# 3. Authentication vs Authorization

| Authentication    | Authorization      |
| ----------------- | ------------------ |
| Verifies identity | Checks permissions |
| "Who are you?"    | "What can you do?" |
| Login             | Access control     |
| Password/JWT      | Roles/permissions  |

Typical flow:

```text
Login
 ↓
Authentication
 ↓
JWT
 ↓
Authorization
 ↓
RBAC
 ↓
Protected Resource
```

---

# 4. What is a role?

A role represents a category of permissions assigned to a user.

Examples:

```text
admin
manager
staff
user
```

Example user:

```json
{
  "name": "Veera",
  "role": "admin"
}
```

---

# 5. What is a permission?

A permission represents a specific allowed action.

Examples:

```text
users:read
users:create
users:update
users:delete

products:read
products:create
products:update
products:delete
```

This provides more granular access control than roles alone.

---

# 6. Role vs Permission

```text
Role
 ↓
Collection of permissions
 ↓
Allowed actions
```

Example:

```text
Admin
 ↓
products:create
products:read
products:update
products:delete
```

---

# 7. How does JWT work with RBAC?

Typical flow:

```text
Login
 ↓
Verify Credentials
 ↓
Create JWT
 ↓
JWT contains user identity / relevant claims
 ↓
Request Protected Route
 ↓
Verify JWT
 ↓
Identify User
 ↓
Check Role/Permission
 ↓
Allow or Reject
```

Example payload:

```json
{
  "userId": "123",
  "role": "admin"
}
```

---

# 8. What is authentication middleware?

Authentication middleware verifies the user's credentials/token.

```js
const authenticate = (req, res, next) => {
  // verify JWT

  req.user = decoded;

  next();
};
```

It answers:

> Is this request authenticated?

---

# 9. What is authorization middleware?

Authorization middleware checks whether the authenticated user has the required role or permission.

Example:

```js
const authorize =
  (...allowedRoles) =>
  (req, res, next) => {
    if (!allowedRoles.includes(req.user.role)) {
      return res.status(403).json({
        message: "Access denied"
      });
    }

    next();
  };
```

Usage:

```js
router.delete(
  "/products/:id",
  authenticate,
  authorize("admin"),
  deleteProduct
);
```

---

# 10. Why should authentication run before authorization?

Authorization needs to know **who the user is**.

Correct:

```text
Request
 ↓
Authenticate
 ↓
Identify User
 ↓
Authorize
 ↓
Controller
```

Incorrect:

```text
Request
 ↓
Authorize
 ↓
Who is the user?
```

Therefore:

> Authentication normally comes before authorization.

---

# 11. What is role-based middleware?

Example:

```js
const authorize =
  (...roles) =>
  (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({
        message: "Forbidden"
      });
    }

    next();
  };
```

Use:

```js
router.get(
  "/admin/dashboard",
  authenticate,
  authorize("admin"),
  getDashboard
);
```

---

# 12. How do you allow multiple roles?

```js
router.get(
  "/reports",
  authenticate,
  authorize("admin", "manager"),
  getReports
);
```

The middleware allows either role.

```text
admin   → allowed
manager → allowed
user    → forbidden
```

---

# 13. How do you implement permission-based authorization?

Instead of checking only roles:

```js
authorizePermission("products:delete")
```

Example:

```js
const authorizePermission =
  (requiredPermission) =>
  (req, res, next) => {
    if (
      !req.user.permissions?.includes(
        requiredPermission
      )
    ) {
      return res.status(403).json({
        message: "Permission denied"
      });
    }

    next();
  };
```

---

# 14. Where should roles be stored?

Roles can be stored in the user document.

Example:

```js
const userSchema = new mongoose.Schema({
  name: String,

  email: String,

  password: String,

  role: {
    type: String,
    enum: [
      "admin",
      "manager",
      "user"
    ],
    default: "user"
  }
});
```

---

# 15. Where should permissions be stored?

For a simple application:

```js
{
  role: "admin"
}
```

and permissions can be defined in application configuration.

For larger systems, roles and permissions can be separate database entities.

Example:

```text
Role
 ↓
Permissions
 ↓
Resources
```

---

# 16. Simple RBAC database design

A simple approach:

```text
users
 ├── _id
 ├── name
 ├── email
 ├── password
 └── role
```

Example:

```json
{
  "name": "Veera",
  "email": "veera@example.com",
  "role": "admin"
}
```

This is sufficient when the number of roles is small and stable.

---

# 17. More scalable RBAC design

For larger applications:

```text
users
roles
permissions
```

Relationship:

```text
User
 ↓
Role
 ↓
Permissions
```

Example:

```text
Admin
 ↓
products:create
products:update
products:delete
orders:read
users:read
```

---

# 18. What is least privilege?

Least privilege means giving users only the access required for their responsibilities.

Example:

```text
Customer
→ Read products
→ Create own orders

Support Staff
→ Read customer information
→ Manage support tickets

Admin
→ Manage users
→ Manage products
→ Manage orders
```

A user should not receive unnecessary administrative permissions.

---

# 19. What is role hierarchy?

Some systems define roles where a higher role inherits permissions from lower roles.

Example:

```text
Admin
 ↓
Manager
 ↓
Staff
 ↓
User
```

However, hierarchy should be explicitly designed. A role name alone should not automatically imply permissions unless the application defines that relationship.

---

# 20. What happens if a user changes role?

Suppose:

```text
User
role = "user"
```

becomes:

```text
User
role = "admin"
```

If the JWT contains the role, an already-issued token may still contain the old role until it expires or is replaced.

Therefore, security-sensitive systems may verify current authorization against server-side user state instead of trusting stale role claims indefinitely.

---

# 21. Should you trust the role sent by the frontend?

No.

Never do this:

```js
const { role } = req.body;
```

and use it for authorization.

The client controls the request.

Instead:

```text
Request
 ↓
Verified JWT
 ↓
Authenticated user
 ↓
Server-side role/permission check
 ↓
Authorization decision
```

---

# 22. Why is frontend role checking not enough?

React can hide an admin button:

```jsx
{user.role === "admin" && (
  <button>Delete</button>
)}
```

This improves the user interface, but it is **not security**.

An attacker can directly call the API.

Therefore:

```text
Frontend authorization
→ UI/UX

Backend authorization
→ Security boundary
```

---

# 23. How do you protect an admin route?

```js
router.delete(
  "/products/:id",
  authenticate,
  authorize("admin"),
  deleteProduct
);
```

Flow:

```text
Request
 ↓
JWT Verification
 ↓
Authenticated User
 ↓
Role Check
 ↓
Admin?
 ├── Yes → Controller
 └── No  → 403
```

---

# 24. What status code should RBAC return?

When the user is authenticated but lacks permission:

```text
403 Forbidden
```

Example:

```js
return res.status(403).json({
  message: "You do not have permission"
});
```

If authentication itself is missing or invalid:

```text
401 Unauthorized
```

---

# 25. How do you combine JWT and RBAC?

A clean Express structure:

```text
routes/
   ↓
authenticate
   ↓
authorize
   ↓
controller
```

Example:

```js
router.post(
  "/products",
  authenticate,
  authorize("admin", "manager"),
  createProduct
);
```

---

# 26. What is permission-based RBAC useful for?

Imagine:

```text
Admin
Manager
Editor
Support
```

Instead of writing many role checks:

```js
authorize("admin")
```

you can use permissions:

```text
products:create
products:update
orders:read
users:update
```

This allows more granular access control.

---

# 27. How do you prevent privilege escalation?

Important practices:

```text
Never trust client-provided roles
Verify JWT signatures
Validate permissions on the server
Restrict role-management endpoints
Use least privilege
Validate input
Protect admin routes
Audit sensitive actions
Secure password/account recovery flows
```

---

# 28. What is RBAC middleware flow?

```text
Client
  ↓
HTTP Request
  ↓
JWT Authentication
  ↓
req.user
  ↓
Role / Permission Middleware
  ↓
Access Check
  ↓
Controller
  ↓
Database
  ↓
Response
```

---

# 29. Example: Complete JWT + RBAC Flow

### Authentication Middleware

```js
const jwt = require("jsonwebtoken");

const authenticate = (req, res, next) => {
  const authHeader = req.headers.authorization;

  if (!authHeader?.startsWith("Bearer ")) {
    return res.status(401).json({
      message: "Authentication required"
    });
  }

  const token = authHeader.split(" ")[1];

  try {
    const decoded = jwt.verify(
      token,
      process.env.JWT_SECRET
    );

    req.user = decoded;

    next();
  } catch (error) {
    return res.status(401).json({
      message: "Invalid or expired token"
    });
  }
};
```

### Authorization Middleware

```js
const authorize =
  (...roles) =>
  (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({
        message: "Access denied"
      });
    }

    next();
  };
```

### Protected Route

```js
router.delete(
  "/products/:id",
  authenticate,
  authorize("admin"),
  deleteProduct
);
```

---

# 30. What is the difference between RBAC and authentication?

```text
Authentication
→ Identifies the user.

RBAC
→ Determines what the authenticated user can access.
```

Example:

```text
Login
 ↓
Authentication
 ↓
User = Veera
 ↓
Role = Admin
 ↓
RBAC
 ↓
Can delete product?
 ↓
Yes
```

---

# 31. RBAC vs ABAC

### RBAC

Access is primarily based on roles.

```text
Admin → Delete Product
User  → View Product
```

### ABAC

Access decisions can consider attributes such as:

```text
User
Resource
Action
Environment
```

Example:

```text
User department = Finance
AND
Resource department = Finance
AND
Action = read
```

RBAC is generally simpler. ABAC can support more complex authorization rules.

---

# 32. What should an admin panel backend protect?

Typical protected operations include:

```text
User Management
Product Management
Order Management
Inventory Management
Coupon Management
Reports
Role Management
Permission Management
Audit Logs
```

Each operation should have an explicit authorization rule.

---

# 33. What is an audit log?

An audit log records important actions performed by users.

Example:

```json
{
  "userId": "123",
  "action": "DELETE_PRODUCT",
  "resourceId": "456",
  "timestamp": "2026-09-27T10:00:00Z"
}
```

Useful for:

* Security investigations
* Administrative tracking
* Compliance requirements
* Debugging

---

# 34. How should role management be protected?

Role-management APIs are highly sensitive.

Example:

```text
POST /api/roles
PATCH /api/users/:id/role
DELETE /api/roles/:id
```

These endpoints should require appropriate administrative permissions.

Do not allow a normal user to modify their own role through a client request.

---

# 35. What are common RBAC security mistakes?

Avoid:

```text
Trusting role from request body
Relying only on frontend checks
Forgetting authorization middleware
Using only UI restrictions
Giving every user admin permissions
Not protecting role-management endpoints
Using stale authorization information indefinitely
Missing audit logs for sensitive operations
```

---

# RBAC Revision Checklist

## Core

* [ ] Authorization
* [ ] RBAC
* [ ] Role
* [ ] Permission
* [ ] Authentication vs authorization
* [ ] Role vs permission

## JWT + RBAC

* [ ] JWT authentication
* [ ] Authentication middleware
* [ ] Authorization middleware
* [ ] `req.user`
* [ ] Role checking
* [ ] Permission checking
* [ ] 401 vs 403

## Security

* [ ] Never trust frontend roles
* [ ] Server-side authorization
* [ ] Least privilege
* [ ] Privilege escalation
* [ ] Role management security
* [ ] Audit logs
* [ ] Sensitive admin operations

## Architecture

* [ ] User → Role
* [ ] Role → Permissions
* [ ] Protected routes
* [ ] Middleware order
* [ ] Role-based authorization
* [ ] Permission-based authorization
* [ ] RBAC vs ABAC

---

# Final Authentication + Authorization Flow

This is the most important flow to understand for your MERN backend interviews:

```text
                 REGISTER
                    ↓
             Hash Password
                    ↓
              Save User
                    ↓
                  LOGIN
                    ↓
          Verify Email + Password
                    ↓
            Generate JWT
                    ↓
                 Client
                    ↓
        ┌──────────────────────┐
        │ Protected API Request │
        └──────────────────────┘
                    ↓
             JWT Middleware
                    ↓
             Verify JWT
                    ↓
                req.user
                    ↓
          Authorization Middleware
                    ↓
           Role / Permission Check
              ↙             ↘
           Allowed          Denied
              ↓                ↓
         Controller           403
              ↓
           Service
              ↓
          MongoDB
              ↓
          Response
```

### The 4 Questions You Must Answer in an Interview

```text
1. Authentication?
   → Who is the user?

2. JWT?
   → How do we securely represent authenticated identity
     in an API request?

3. Authorization?
   → What is the authenticated user allowed to do?

4. RBAC?
   → How do we control access based on roles/permissions?
```

### Final Backend Security Model

```text
Password
   ↓
bcrypt / Argon2
   ↓
Authentication
   ↓
JWT
   ↓
Authentication Middleware
   ↓
User Identity
   ↓
RBAC / Permissions
   ↓
Authorization
   ↓
Protected Controller
   ↓
Database
```

> **Main interview goal:** Be able to explain the complete difference between authentication and authorization, then show how JWT identifies the user and RBAC controls what that user can access.
