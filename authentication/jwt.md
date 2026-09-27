# JWT Authentication Interview Questions

> **Level:** Fresher / Junior Backend Developer
> **Focus:** Important JWT authentication concepts + commonly asked interview questions
> **Prerequisite:** Node.js + Express.js + MongoDB

---

# 1. What is Authentication?

Authentication verifies **who the user is**.

Example:

```text
User
 ↓
Email + Password
 ↓
Server verifies credentials
 ↓
User authenticated
```

Common authentication methods:

* Session-based authentication
* JWT-based authentication
* OAuth
* API keys

---

# 2. What is JWT?

JWT stands for **JSON Web Token**.

It is a compact token format commonly used to securely transmit claims between parties.

JWTs are commonly used for authentication:

```text
Login
  ↓
Verify credentials
  ↓
Create JWT
  ↓
Client receives token
  ↓
Client sends token with protected requests
  ↓
Server verifies token
```

---

# 3. Why is JWT used?

JWT can be used to:

* Identify authenticated users
* Protect API routes
* Carry claims such as user ID and role
* Build stateless authentication systems

Example payload:

```json
{
  "userId": "123",
  "role": "user"
}
```

---

# 4. What are the three parts of a JWT?

A JWT has three parts separated by dots:

```text
HEADER.PAYLOAD.SIGNATURE
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

### Header

Contains information such as the signing algorithm.

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload

Contains claims.

```json
{
  "userId": "123",
  "role": "user"
}
```

### Signature

Used to verify that the token was signed by a trusted party and has not been modified.

---

# 5. Is JWT encrypted?

**Not by default.**

A normal signed JWT is encoded and signed, not encrypted.

Therefore, don't put sensitive information such as:

```text
Passwords
Credit card numbers
Private secrets
```

inside a normal JWT payload.

### Important Point

> JWT payload data should be treated as readable by anyone who possesses the token.

---

# 6. What is a JWT signature?

The signature helps verify token integrity and authenticity.

Conceptually:

```text
Header + Payload + Secret
          ↓
       Signature
```

When the server receives the token, it verifies the signature.

If someone modifies the payload, signature verification should fail.

---

# 7. What is a JWT secret?

A JWT secret is a secret value used to sign and verify tokens when using a symmetric signing algorithm such as HS256.

Example:

```text
JWT_SECRET=long_random_secret
```

In Node.js:

```js
const token = jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET
);
```

Never hard-code production secrets or commit them to GitHub.

---

# 8. How does JWT authentication work?

Typical login flow:

```text
Client
  ↓
POST /api/auth/login
  ↓
Express
  ↓
Find user
  ↓
Compare password
  ↓
Create JWT
  ↓
Return token
```

Protected request:

```text
Client
  ↓
GET /api/profile
Authorization: Bearer TOKEN
  ↓
JWT Middleware
  ↓
Verify token
  ↓
Attach user information
  ↓
Controller
  ↓
Response
```

---

# 9. How do you create a JWT in Node.js?

Install:

```bash
npm install jsonwebtoken
```

Example:

```js
const jwt = require("jsonwebtoken");

const token = jwt.sign(
  {
    userId: user._id,
    role: user.role
  },
  process.env.JWT_SECRET,
  {
    expiresIn: "1h"
  }
);

console.log(token);
```

---

# 10. How do you verify a JWT?

```js
const jwt = require("jsonwebtoken");

try {
  const decoded = jwt.verify(
    token,
    process.env.JWT_SECRET
  );

  console.log(decoded);
} catch (error) {
  console.log("Invalid or expired token");
}
```

`jwt.verify()` checks the token's signature and validates relevant registered claims such as expiration.

---

# 11. What is JWT expiration?

A JWT can contain an expiration time.

```js
const token = jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET,
  {
    expiresIn: "15m"
  }
);
```

After expiration, the token should no longer be accepted for authentication.

---

# 12. What are access tokens and refresh tokens?

### Access Token

Used to access protected resources.

```text
Short-lived
```

Example:

```text
15 minutes
```

### Refresh Token

Used to obtain a new access token.

```text
Longer-lived
```

Example architecture:

```text
Login
 ↓
Access Token + Refresh Token
 ↓
Access Token expires
 ↓
Refresh Token
 ↓
New Access Token
```

Exact lifetimes should be chosen according to the application's security requirements.

---

# 13. Why use short-lived access tokens?

Short-lived access tokens reduce the period during which a stolen access token can be used.

Example:

```text
Access Token
   ↓
15 minutes
   ↓
Expires
```

The refresh mechanism can then issue another access token when appropriate.

---

# 14. What is the Authorization header?

A common way to send a bearer access token is:

```text
Authorization: Bearer <JWT>
```

Express:

```js
const authHeader = req.headers.authorization;
```

Extract the token:

```js
const token = authHeader?.startsWith("Bearer ")
  ? authHeader.split(" ")[1]
  : null;
```

---

# 15. How do you create JWT authentication middleware?

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

module.exports = authenticate;
```

Then:

```js
router.get(
  "/profile",
  authenticate,
  getProfile
);
```

---

# 16. Why attach the decoded user to `req`?

After verification:

```js
req.user = decoded;
```

The controller can access the authenticated user's information.

```js
const getProfile = (req, res) => {
  console.log(req.user.userId);

  res.json({
    message: "Profile"
  });
};
```

This avoids verifying the same token repeatedly within the same request.

---

# 17. What is stateless authentication?

In a stateless JWT authentication model, the server does not need to maintain a traditional login session for every access token.

The request contains the authentication token:

```text
Request
  ↓
JWT
  ↓
Server verifies token
  ↓
User authenticated
```

However, real systems may still maintain server-side state for refresh-token rotation, revocation, sessions, or other security controls.

---

# 18. JWT vs Session Authentication

| JWT                                   | Session                                |
| ------------------------------------- | -------------------------------------- |
| Token-based                           | Session-based                          |
| Commonly stateless for access tokens  | Server stores session state            |
| Token sent with requests              | Session identifier commonly sent       |
| Useful for APIs                       | Common for web applications            |
| Revocation requires additional design | Server can invalidate session directly |

Neither approach is universally correct; architecture and security requirements determine the choice.

---

# 19. Where should JWT tokens be stored?

There is no single storage method that is safe for every architecture.

Common approaches include:

### HttpOnly Cookie

```text
Browser
  ↓
HttpOnly Cookie
  ↓
Server
```

JavaScript cannot directly read an HttpOnly cookie.

### Memory

The token can be kept in application memory.

### Browser Storage

`localStorage` and `sessionStorage` are accessible to JavaScript, so an XSS vulnerability can expose tokens stored there.

### Interview Point

> Token storage should be selected based on the application's threat model. HttpOnly, Secure, appropriately configured cookies are commonly used for browser-based authentication.

---

# 20. What is an HttpOnly cookie?

An HttpOnly cookie cannot be accessed by client-side JavaScript through `document.cookie`.

Example:

```js
res.cookie("refreshToken", token, {
  httpOnly: true,
  secure: true,
  sameSite: "strict"
});
```

This can reduce exposure to token theft through certain XSS scenarios.

---

# 21. What does `Secure` mean for cookies?

A `Secure` cookie is sent only over HTTPS connections.

```js
{
  secure: true
}
```

Production authentication cookies should generally use HTTPS.

---

# 22. What is `SameSite`?

`SameSite` controls when cookies are sent in cross-site contexts.

Common values:

```text
Strict
Lax
None
```

Example:

```js
{
  sameSite: "strict"
}
```

The appropriate setting depends on the application's frontend/backend architecture.

---

# 23. Should passwords be stored inside JWT?

No.

Never store:

```text
Password
Password hash
```

inside the JWT payload.

The JWT should contain only the claims necessary for the application.

Example:

```json
{
  "userId": "123",
  "role": "user"
}
```

---

# 24. How should passwords be stored?

Passwords should **never be stored as plain text**.

Use a password hashing algorithm such as:

```text
bcrypt
Argon2
```

Example with bcrypt:

```js
const bcrypt = require("bcrypt");

const hashedPassword = await bcrypt.hash(
  password,
  12
);
```

Verify:

```js
const isMatch = await bcrypt.compare(
  password,
  user.password
);
```

---

# 25. What happens if the JWT is modified?

Suppose the original token contains:

```json
{
  "role": "user"
}
```

An attacker changes it to:

```json
{
  "role": "admin"
}
```

The original signature no longer matches the modified content.

JWT verification should fail.

```js
jwt.verify(token, secret);
```

---

# 26. Can a JWT be revoked?

A normal self-contained JWT is not automatically revocable before its expiration.

Applications can implement revocation strategies such as:

* Short-lived access tokens
* Refresh-token rotation
* Server-side refresh-token/session records
* Token deny lists where appropriate
* User/session versioning

The correct approach depends on the application's security requirements.

---

# 27. What happens when an access token expires?

The API should reject the expired access token.

```text
Access Token
    ↓
Expired
    ↓
401 Unauthorized
```

If refresh tokens are implemented:

```text
Expired Access Token
       ↓
Refresh Token
       ↓
New Access Token
```

---

# 28. What is a refresh-token rotation?

Refresh-token rotation means issuing a new refresh token when a refresh operation succeeds and invalidating the previous refresh token.

Conceptually:

```text
Refresh Token A
      ↓
Refresh Request
      ↓
Access Token B
Refresh Token C
      ↓
Refresh Token A invalidated
```

This can reduce the impact of refresh-token theft when implemented correctly.

---

# 29. What should happen during logout?

The exact implementation depends on the authentication architecture.

For cookie-based refresh tokens, a server can:

* Clear the authentication cookie
* Revoke/delete the refresh-token record
* Invalidate the session

For purely self-contained access tokens, the client can discard the token, but a server-side revocation strategy may be required if immediate invalidation is needed.

---

# 30. What is the difference between 401 and 403?

### 401 Unauthorized

The request lacks valid authentication credentials.

Examples:

```text
Missing token
Invalid token
Expired token
```

### 403 Forbidden

The user is authenticated but does not have permission to perform the requested action.

Example:

```text
Authenticated USER
      ↓
DELETE /api/products/123
      ↓
No required permission
      ↓
403 Forbidden
```

---

# JWT Revision Checklist

* [ ] Authentication
* [ ] JWT
* [ ] Header
* [ ] Payload
* [ ] Signature
* [ ] JWT secret
* [ ] `jwt.sign()`
* [ ] `jwt.verify()`
* [ ] Expiration
* [ ] Access token
* [ ] Refresh token
* [ ] Authorization header
* [ ] Bearer token
* [ ] JWT middleware
* [ ] `req.user`
* [ ] Stateless authentication
* [ ] JWT vs sessions
* [ ] Cookie security
* [ ] HttpOnly
* [ ] Secure
* [ ] SameSite
* [ ] Password hashing
* [ ] Token revocation
* [ ] Refresh-token rotation
* [ ] Logout
* [ ] 401 vs 403

---

# JWT Authentication Flow

Be able to explain this completely:

```text
                REGISTER
                   ↓
          Hash Password
                   ↓
             Save User
                   ↓
                 LOGIN
                   ↓
          Verify Password
                   ↓
        Generate Access Token
                   ↓
        Generate Refresh Token
                   ↓
              Client
                   ↓
        Protected API Request
                   ↓
        Authorization: Bearer JWT
                   ↓
         Authentication Middleware
                   ↓
           Verify JWT
                   ↓
              req.user
                   ↓
             Controller
                   ↓
              Response
```

### One-Line Interview Answer

> **JWT is a signed token format commonly used for API authentication, where the server verifies the token on protected requests and uses its validated claims to identify the authenticated user.**
