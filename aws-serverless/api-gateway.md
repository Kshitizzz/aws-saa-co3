# Amazon API Gateway – SAA-C03 Exam Prep Guide

## Memory Hook  
- “API Gateway = secure, scalable front door for your backend”

---

## ✅ What Is API Gateway?

A fully managed service that makes it easy to **create, publish, secure, and monitor APIs**.  
It sits in front of services like:
- AWS Lambda
- EC2
- VPC Link (private services)
- HTTP endpoints (external services)

---

## ✅ Core API Types

| Type                  | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **REST API**           | ✅ Traditional RESTful APIs (regional, edge-optimized, or private)           |
| **HTTP API**           | ✅ Simpler, cheaper, faster — preferred for most Lambda integrations         |
| **WebSocket API**      | ✅ Bi-directional communication (chat, IoT)                                   |

🧠 For SAA-C03, focus on **REST vs HTTP API**

---

## 📦 REST vs HTTP API (Exam Angle)

| Feature                     | REST API                    | HTTP API                       |
|-----------------------------|-----------------------------|--------------------------------|
| Price                       | 💸 More expensive            | ✅ Cheaper (70%+ savings)       |
| Caching                     | ✅ Yes (with API Gateway cache) | ❌ No                         |
| Fine-grained auth (IAM, Cognito, Lambda auth) | ✅ Full support | ✅ Limited support            |
| VPC Link support            | ✅ Yes                      | ✅ Yes                          |
| Usage plans & API keys      | ✅ Yes                      | ❌ Not supported                |
| Integration flexibility     | ✅ More features             | ✅ Faster, simpler              |

---

## 🔐 Authorization Options

| Method           | Description                                        |
|------------------|----------------------------------------------------|
| **IAM**          | Used for signed requests from AWS SDKs/CLI         |
| **Cognito**      | Authenticate users via User Pools                  |
| **Lambda Authorizer** | Custom token/auth header validation         |
| **API Key**      | Throttling & tracking (not secure authentication)  |

---

## 🔧 Integration Types

| Integration Target         | Description                                           |
|-----------------------------|-------------------------------------------------------|
| **Lambda Function**         | Serverless backend                                    |
| **HTTP/HTTPS Endpoint**     | Forward request to external APIs                      |
| **AWS Service (e.g., DynamoDB)** | Call AWS services with IAM role credentials     |
| **VPC Link**                | Access private resources in VPC (e.g., ALB, EC2)      |

---

## 🔄 Throttling & Rate Limiting

- Set via:
  - Stage-level configuration
  - Usage Plans (REST APIs only)
- Protects downstream systems from overload

---

## 📊 Monitoring & Logging

- **CloudWatch Metrics**: Latency, error count, request count
- **CloudWatch Logs**: Full request/response logging (must be enabled)
- **X-Ray**: End-to-end tracing for debugging performance bottlenecks

---

## 🛡️ Security Features

- TLS termination
- WAF integration (only with REST API)
- Throttling limits
- IP whitelisting/blacklisting via Lambda authorizers
- CORS headers configurable per method

---

## 🧠 Exam Nuances & Traps

- ❗ **REST API supports API keys** and usage plans → HTTP API does not
- ❗ **Caching is only available on REST APIs**
- ✅ Use **IAM roles** to let API Gateway invoke backend services securely
- ✅ API Gateway can **invoke private services** via **VPC Link**
- ✅ API Gateway + Lambda is a **fully serverless microservice pattern**

---

## 📌 Exam Pointers

- “Need fast, cheap API with Lambda backend and JWT auth?” → ✅ HTTP API + Cognito
- “Want to throttle users by API key?” → ✅ REST API + Usage Plan
- “Expose private VPC service via public API?” → ✅ Use VPC Link
- “Secure backend with IAM roles only?” → ✅ IAM Authorization
- “Enable caching to reduce backend calls?” → ✅ REST API only (not HTTP API)

---

## 🛠️ Design Patterns

- **API Gateway + Lambda + DynamoDB** → Serverless CRUD
- **API Gateway + VPC Link + ECS** → Secure REST API for microservices
- **API Gateway + S3 + CloudFront** → Hybrid static + dynamic app

