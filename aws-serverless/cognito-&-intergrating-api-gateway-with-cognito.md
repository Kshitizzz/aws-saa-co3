# API Gateway + AWS Cognito + Authorization – Deep Dive + Architecture

## Memory Hook  
- “Cognito = Identity brain of AWS”  
- “API Gateway enforces, Cognito authenticates”

---

## ✅ What Is AWS Cognito?

A fully managed identity provider that handles:

| Feature                        | Description                          |
|-------------------------------|--------------------------------------|
| **User Pools**                | ✅ User directory + login + JWT token issuing via Cognito User Pools (CUPs)
| **Identity Pools**            | ✅ Federated identities (e.g., Google, Facebook) → temporary AWS credentials via Cognito Identity Pools (CIPs)
| **Hosted UI**                 | ✅ Pre-built login/signup UI          |
| **OIDC & OAuth2 Support**     | ✅ Integrates with external IdPs      |
| **MFA, password recovery**    | ✅ Built-in                          |

🧠 User Pool = *who are you*  
🧠 Identity Pool = *what can you access in AWS*

---

## 🔐 API Gateway Authorization Options – Deep Dive

| Method               | Enforces | Use Case Example                                       |
|----------------------|----------|--------------------------------------------------------|
| **IAM Auth**         | ✅ Yes   | AWS SDK / CLI calls signed with SigV4 (e.g., Lambda, S3)|
| **Cognito JWT Auth** | ✅ Yes   | Single Sign-On, secure login via Cognito User Pool     |
| **Lambda Authorizer**| ✅ Yes   | Custom headers, JWTs from non-Cognito IdPs             |
| **API Key**          | ❌ No    | Usage tracking & rate limiting only                    |
| **No Auth**          | ❌ No    | Public APIs only                                       |

---

## 🧠 Cognito User Pool + API Gateway (JWT Flow)

1. User logs in to **Cognito User Pool**
2. Cognito returns **ID token (JWT)** and **access token**
3. API Gateway requires `Authorization: Bearer <JWT>`
4. API Gateway **verifies token signature + claims**
5. ✅ If valid → forwards request to backend

---

## 🧠 Lambda Authorizer

> A Lambda function that runs **before the request hits your backend** to evaluate custom auth logic

Use it when:
- Using **non-Cognito tokens**
- Need **custom roles / logic** (e.g., ABAC, geo-checks)
- Want to inject user context into headers

Returns:
- `principalId`
- Optional `context`
- `policyDocument` (IAM-like allow/deny)

---

## 📐 Real-World Multi-Tier Architecture Example

### Goal: Build a secure, scalable SaaS-like app

#### Frontend (React/Next.js/Vue)
- Hosted on S3 + CloudFront
- Calls backend via **API Gateway**

#### Auth
- Uses **Cognito Hosted UI** or embedded login form
- After login → receives **JWT token**
- JWT stored in browser → passed as `Authorization: Bearer ...` header

#### API Layer
- **API Gateway (HTTP API)** with:
  - **Cognito JWT Auth**
  - CORS configured
  - Rate limiting

#### Backend
- **AWS Lambda**
  - Stateless compute
  - Runs API logic
- **DynamoDB / Aurora Serverless**
  - Stores user/session/app data

#### Optional: Private resources
- Expose EC2/ECS services via **VPC Link**

---

## 🧩 Sample Request Flow

1. User logs in via Cognito → gets token
2. Sends request to API Gateway with token
3. API Gateway verifies JWT with Cognito
4. If valid, forwards to Lambda
5. Lambda runs logic, queries DB
6. Returns response to client

---

## 🔐 Security Best Practices

- ✅ Always validate JWT expiry + signature
- ✅ Use **short token lifetimes** + refresh tokens
- ✅ Use **authorizer context** to pass user info to Lambda (e.g., userId, role)
- ✅ Rate limit + WAF protect APIs
- ✅ Use **custom scopes + groups** in Cognito for RBAC

---

## 📌 Exam Pointers

- “Want to use Cognito with OAuth2-style login + JWT verification?” → ✅ Use Cognito User Pool with API Gateway JWT auth
- “Need custom authorization logic from a third-party token?” → ✅ Lambda Authorizer
- “Track request quota per user?” → ✅ Use API Keys + Usage Plans (REST API only)
- “Federate Google users + assign AWS access?” → ✅ Cognito Identity Pool + AssumeRole
- “Frontend login + API Gateway integration?” → ✅ Cognito + JWT + API Gateway (HTTP API)

---

## ✅ Summary Table

| Component              | Role                                                       |
|------------------------|------------------------------------------------------------|
| **Cognito User Pool**  | User auth, JWT issuance                                    |
| **API Gateway**        | Verifies JWT, routes request                               |
| **Lambda**             | Business logic execution                                   |
| **DynamoDB**           | Data store                                                 |
| **CloudFront + S3**    | Frontend hosting                                           |
| **VPC Link (optional)**| Access to private services                                 |
| **WAF + Logging**      | Protection + observability                                 |

