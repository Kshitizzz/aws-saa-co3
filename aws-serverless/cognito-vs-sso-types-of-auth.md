# Cognito vs AWS SSO + JWT vs Other Auth Methods

## Memory Hook  
- “Cognito = App login for your users”  
- “AWS SSO = Login for your employees”  
- “JWT = Ticket to ride — stateless, signed, portable”

---

## ✅ Cognito vs AWS IAM Identity Center (formerly AWS SSO)

| Feature                      | **Amazon Cognito**                                 | **AWS SSO (Identity Center)**                           |
|------------------------------|----------------------------------------------------|----------------------------------------------------------|
| **Primary Use Case**         | ✅ Customer-facing applications                    | ✅ Workforce access to AWS or SaaS apps                  |
| **User Source**              | Cognito User Pools (self-managed) + social logins | IAM Identity Center + AD, SAML, OIDC IdPs               |
| **Federated Login**          | ✅ Google, Facebook, Apple, SAML                    | ✅ SAML, OIDC (Azure AD, Okta, etc.)                     |
| **Application Access**       | Mobile/Web apps                                    | AWS Console, CLI, 3rd-party SaaS (e.g., Salesforce)     |
| **Token Type Returned**      | JWTs (ID, access, refresh)                         | SAML/OIDC tokens (for AWS federation or SSO)            |
| **Custom App Auth Flows**    | ✅ Yes (OAuth2, JWT)                               | ❌ No — prebuilt for workforce login                     |
| **UI Hosting**               | ✅ Cognito Hosted UI                               | ❌ No UI (login portal is fixed per org)                 |

### 🧠 Key Insight  
- **Use Cognito** for public **user signup/login flows** (web/mobile apps)  
- **Use IAM Identity Center** for **employee and cross-account AWS access**

---

## ✅ Why Use Cognito If SSO Also Supports Federated Logins?

> Because **Cognito gives you app-level user management, tokens, flows, and UI**, while AWS SSO is built for AWS account access and enterprise federation.

| Use Case                                | Tool                      |
|-----------------------------------------|----------------------------|
| Login to **your app** with Facebook     | ✅ Cognito (OAuth + UI)    |
| Login to **AWS Console** with Azure AD  | ✅ IAM Identity Center     |
| Authenticate users in **a React SPA**   | ✅ Cognito (JWT + Hosted UI) |
| Give devs access to multiple AWS accounts | ✅ IAM Identity Center     |

---

## 🔐 What Is JWT (JSON Web Token)?

> A **self-contained, signed token** that holds user claims (identity, groups, scopes)  
> Used in stateless, secure APIs.

### Structure:

<Header>.<Payload>.<Signature>
Example Payload:

{
  "sub": "1234567890",
  "email": "user@example.com",
  "exp": 1700000000
}
Key Properties:
✅ Signed (via HMAC or RSA)

✅ Portable across services (stateless)

❌ Not encrypted by default — can be read but not tampered

🔑 JWT-Based Auth Flow (OAuth2 / OpenID Connect)
User logs in to Cognito (or any IdP)

Receives ID token (JWT) + access token (JWT)

Sends token to API in Authorization: Bearer <token>

Backend or API Gateway validates signature + claims

Access granted if valid and unexpired

🔐 Other Auth Types – Compared
Method	| What It Is	| Pros	| Cons	| Use When
JWT	| Stateless token with signed claims	| ✅ Fast, portable, cacheable	| ❌ Must handle expiry/rotation	| Public APIs, mobile/web apps
Session Cookie	| Server-stored session ID	| ✅ Easy for websites	| ❌ Requires sticky sessions	| Classic web login
OAuth 2.0	| Authorization protocol (tokens + scopes)	| ✅ Delegation via Google, FB, etc.	| ❌ Complex flow	| Third-party logins
SAML 2.0	| Enterprise login via XML-based IdP	| ✅ Compatible with Okta, Azure AD	| ❌ Heavy, older, not ideal for apps	| B2B / Workforce SSO
Basic Auth	| username:password in headers	| ✅ Simple	| ❌ No rotation, no RBAC	| Quick internal tools
API Key	| Static identifier for requests	| ✅ Easy to track	| ❌ Not secure for identity	| Rate limiting, internal usage
IAM Signature v4	| AWS-style signed requests	| ✅ Secure for AWS calls	| ❌ Not user-friendly for APIs	| AWS SDK/API Gateway w/ IAM auth

📌 Exam Pointers
“Need public user authentication + JWT-based login?” → ✅ Use Cognito

“Enable SSO to AWS accounts for employees via Okta?” → ✅ IAM Identity Center

“User gets a JWT after login — where does it come from?” → ✅ Cognito User Pool (or IdP)

“API Gateway needs to verify user identity from token?” → ✅ Enable JWT Authorizer

“Difference between SAML and OIDC?” → ✅ SAML = XML; OIDC = JSON + JWT (OAuth2)