# Authentication Interview Questions and Answers (MERN Stack)

## 1. What is Authentication?

Authentication is the process of verifying the identity of a user.

For example, when a user logs in using an email and password, the application verifies those credentials before allowing access.

## 2. What is Authorization?

Authorization determines what an authenticated user is allowed to access or perform.

For example, an admin can manage users, while a normal user can only access their own account.

## 3. What is the difference between Authentication and Authorization?

| Authentication | Authorization |
|---|---|
| Verifies user identity | Checks user permissions |
| Happens first | Happens after authentication |
| Example: Login | Example: Admin access |
| Answers "Who are you?" | Answers "What can you access?" |

## 4. How does Authentication work in a MERN application?

A typical authentication flow:

1. User enters email and password.
2. React sends credentials to the Express API.
3. Express validates the input.
4. Backend finds the user in MongoDB.
5. Password is compared with the stored hash using bcrypt.
6. If valid, the backend generates an authentication token.
7. The token is sent to the client, commonly through an HttpOnly cookie.
8. Protected API requests include the authentication credential.
9. Middleware verifies the credential before allowing access.

## 5. What is Password Hashing?

Password hashing converts a password into a one-way cryptographic hash.

Instead of storing the original password, applications store its hash in the database.

During login, the submitted password is compared against the stored hash.

## 6. What is bcrypt?

bcrypt is a password-hashing library used to securely hash passwords.

It includes a salt and a configurable work factor, making password cracking more expensive.

Common methods:

- `bcrypt.hash()` – hashes a password.
- `bcrypt.compare()` – compares a password with its stored hash.
- `bcrypt.genSalt()` – generates a salt.

## 7. What is Salt in Password Hashing?

A salt is a random value added during password hashing.

It ensures that identical passwords produce different hashes and makes precomputed hash attacks more difficult.

bcrypt automatically handles salt generation and storage as part of its hash format.

## 8. Why should we never store plain-text passwords?

Plain-text passwords expose users' credentials if the database is compromised.

Applications should store passwords using secure, salted password hashing algorithms such as bcrypt or Argon2.

## 9. What is JWT?

JWT stands for JSON Web Token.

It is a compact token format used to securely transmit claims between parties. In web applications, it is commonly used to carry authenticated user information.

JWT consists of three parts:

1. Header
2. Payload
3. Signature

## 10. What are the three parts of a JWT?

- **Header:** Contains the token type and signing algorithm.
- **Payload:** Contains claims such as user ID, role, and expiration.
- **Signature:** Helps verify that the token has not been modified.

The three parts are separated by dots.

## 11. Is JWT encrypted?

No. A typical signed JWT is not encrypted.

Its header and payload can be decoded and read. The signature provides integrity verification, not confidentiality.

Never store passwords or sensitive personal information in a JWT payload.

## 12. How do you generate a JWT in Node.js?

We commonly use the `jsonwebtoken` package.

```javascript
import jwt from "jsonwebtoken";

const generateToken = (user) => {
  return jwt.sign(
    {
      id: user._id,
      role: user.role,
    },
    process.env.JWT_SECRET,
    {
      expiresIn: "1d",
    }
  );
};
```

The secret should be stored in environment variables, not hardcoded.

## 13. How do you verify a JWT?

We use `jwt.verify()` from the `jsonwebtoken` package.

```javascript
import jwt from "jsonwebtoken";

const decoded = jwt.verify(token, process.env.JWT_SECRET);
```

It verifies the signature and checks registered claims such as expiration.

If verification fails, the application should reject the request.

## 14. What is JWT Middleware?

JWT middleware is an Express middleware function that verifies the user's authentication token before allowing access to protected routes.

Typical responsibilities:

1. Read the token from the request.
2. Verify the token.
3. Identify the authenticated user.
4. Attach user information to `req.user`.
5. Call `next()` if authentication succeeds.

## 15. What is the Authorization Header?

The Authorization header carries authentication credentials in an HTTP request.

A common JWT format is:

```http
Authorization: Bearer <token>
```

The backend extracts and verifies the token before processing a protected request.

## 16. What is the difference between Access Token and Refresh Token?

| Access Token | Refresh Token |
|---|---|
| Used to access protected APIs | Used to obtain new access tokens |
| Short expiration time | Longer expiration time |
| Sent with API requests | Sent only to the refresh endpoint |
| Limits exposure if compromised | Must be protected carefully |

## 17. What is the difference between JWT Authentication and Session Authentication?

**JWT Authentication:**
- Uses signed tokens.
- Commonly uses stateless access-token validation.
- The server does not need to store each access token's session state.

**Session Authentication:**
- Server creates and maintains a session.
- Client stores a session identifier, usually in a cookie.
- Server looks up session information for incoming requests.

## 18. Where should we store JWT tokens in a React application?

A common secure approach is to store authentication tokens in cookies configured with:

- `HttpOnly`
- `Secure`
- `SameSite`

HttpOnly cookies cannot be accessed through JavaScript, reducing token exposure through XSS.

Storing tokens in localStorage is convenient but exposes them to JavaScript if an XSS vulnerability occurs.

The correct approach depends on the application's security requirements and architecture.

## 19. What is an HttpOnly Cookie?

An HttpOnly cookie is a cookie that cannot be accessed through JavaScript using `document.cookie`.

It helps protect authentication tokens from being directly stolen through JavaScript-based XSS attacks.

## 20. What is the difference between localStorage, sessionStorage, and Cookies?

| Feature | localStorage | sessionStorage | Cookies |
|---|---|---|---|
| Storage duration | Until removed | Usually until tab session ends | Configurable |
| JavaScript access | Yes | Yes | Depends on HttpOnly |
| Automatically sent with HTTP requests | No | No | Yes, when applicable |
| Common usage | Persistent client data | Temporary tab data | Authentication and session management |

## 21. What is Refresh Token Rotation?

Refresh token rotation means issuing a new refresh token whenever an existing refresh token is used.

The previous token is invalidated.

This helps detect token reuse and reduces the risk of long-lived refresh-token theft.

## 22. How do you implement Logout in JWT Authentication?

In a cookie-based authentication system:

1. Clear the authentication cookies.
2. Invalidate or revoke the refresh token on the server if refresh-token management is implemented.
3. Reject future requests using revoked credentials.

Simply clearing a cookie does not invalidate a copied, otherwise-valid JWT access token.

## 23. What is OTP Authentication?

OTP stands for One-Time Password.

It is a temporary code used to verify a user's identity, commonly during phone or email verification.

Typical flow:

1. User requests an OTP.
2. Backend generates a random OTP.
3. Backend stores a secure hash with an expiration time.
4. OTP is delivered through an email or SMS provider.
5. User submits the OTP.
6. Backend verifies it and marks the contact as verified.

## 24. What is Two-Factor Authentication (2FA)?

Two-Factor Authentication adds a second verification step to the login process.

For example:

1. User enters an email and password.
2. Application verifies the credentials.
3. User enters an OTP or approves an authenticator challenge.
4. Application grants access after successful verification.

It provides an additional layer of security.

## 25. What is CORS and why is it important in Authentication?

CORS stands for Cross-Origin Resource Sharing.

It controls which origins can access resources from a server through browsers.

For cookie-based authentication across different origins, the backend must configure the allowed origin and credentials correctly.

For example:

```javascript
app.use(
  cors({
    origin: "http://localhost:5173",
    credentials: true,
  })
);
```

The frontend must also send requests with credentials enabled when required.

## 26. What is CSRF?

CSRF stands for Cross-Site Request Forgery.

It is an attack in which a malicious website tricks a user's browser into sending an unwanted request to another website where the user is authenticated.

Common protections include:

- CSRF tokens.
- Appropriate `SameSite` cookie settings.
- Origin and Referer validation where applicable.
- Avoiding state-changing GET requests.

## 27. What is XSS and how does it affect Authentication?

XSS stands for Cross-Site Scripting.

It occurs when attackers inject malicious scripts into a web application.

It can expose sensitive information accessible to JavaScript, including tokens stored in localStorage.

Prevention includes:

- Proper output escaping.
- Avoiding unsafe HTML rendering.
- Content Security Policy.
- Using HttpOnly cookies for authentication tokens.

## 28. What is the difference between HTTP 401 and HTTP 403?

| Status Code | Meaning | Example |
|---|---|---|
| 401 Unauthorized | Authentication is missing or invalid | User sends an invalid JWT |
| 403 Forbidden | User is authenticated but lacks permission | Normal user accesses an admin-only route |

## 29. How do you protect routes in a MERN application?

We protect routes at both frontend and backend levels.

**Frontend:**
- Use React Router protected routes.
- Check authentication state.
- Redirect unauthenticated users to login.

**Backend:**
- Use authentication middleware.
- Verify the JWT or session.
- Check user roles and permissions.
- Reject unauthorized requests.

Backend validation is essential because frontend route protection alone cannot secure an API.

## 30. What are the important security practices for Authentication in MERN?

- Hash passwords using bcrypt or Argon2.
- Never store plain-text passwords.
- Keep JWT secrets in environment variables.
- Use short-lived access tokens.
- Protect refresh tokens.
- Prefer HttpOnly, Secure, and appropriately configured SameSite cookies.
- Validate and sanitize user input.
- Implement login rate limiting.
- Use OTP expiration and attempt limits.
- Prevent XSS and CSRF.
- Use HTTPS in production.
- Never trust user roles sent directly by the frontend.
- Avoid exposing sensitive user information in API responses.

---

## Authentication Flow – Quick Revision

```text
REGISTER
   |
   v
Validate User Input
   |
   v
Hash Password (bcrypt)
   |
   v
Save User in MongoDB
   |
   v
LOGIN
   |
   v
Verify Email and Password
   |
   v
Generate Access Token
   |
   v
Send Authentication Cookie
   |
   v
PROTECTED API REQUEST
   |
   v
Authentication Middleware
   |
   v
Verify Token
   |
   v
Check User Permissions
   |
   v
Allow or Reject Request
```

## Final Interview Preparation Checklist

- [ ] Authentication vs Authorization
- [ ] Password hashing and bcrypt
- [ ] Salt
- [ ] JWT structure and verification
- [ ] Access and Refresh Tokens
- [ ] Authentication middleware
- [ ] Cookies and token storage
- [ ] Session vs JWT
- [ ] OTP and 2FA
- [ ] CORS
- [ ] CSRF and XSS
- [ ] HTTP 401 vs 403
- [ ] Route protection
- [ ] Authentication security practices

**Interview Goal:** Be able to explain the complete MERN authentication flow, implement it independently, and justify the security decisions.
