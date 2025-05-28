# REST API vs HTTP API in AWS API Gateway

## Memory Hook  
- “Both are HTTP-based — but one is turbocharged (REST), the other is lightweight (HTTP API)”

---

## ✅ Are All REST APIs Based on HTTP?

Yes.  
REST is an **architectural style** built over HTTP.  
So when we say **REST API**, we mean an API that:
- Uses HTTP methods (GET, POST, PUT, DELETE, etc.)
- Uses URL paths and query parameters to model resources
- Often returns JSON (but not required)

So:

```
GET /users/123
POST /orders
These are all HTTP-based REST APIs.
```

✅ Then What Is AWS HTTP API vs REST API?
In AWS, "HTTP API" and "REST API" are two different products under API Gateway, even though both speak HTTP!

They differ in:

Features

Cost

Use cases

Performance

🧩 Practical Differences: HTTP API vs REST API in AWS
Feature	REST API (Legacy)	| HTTP API (Modern)
Use Case	Full-featured enterprise APIs	| Lightweight, Lambda-centric apps
Price	💰 More expensive	| ✅ 70% cheaper
Latency	Higher (adds features)	| ✅ Lower (lightweight proxying)
Authorization	✅ IAM, Cognito, Lambda Authorizer, API Key	| ✅ Cognito, JWT Authorizer, Lambda Auth
Stages & Deployment	Manual stage deployment needed	| ✅ Auto-deploy on save
Custom Domain Support	✅ Yes	| ✅ Yes
VPC Link Integration	✅ Yes	| ✅ Yes
CORS	Manual config per method	| ✅ Native support
Usage Plans & API Keys	✅ Yes	| ❌ Not supported
TLS Termination	✅ Both support HTTPS only (TLS)	| ✅ Same (TLS termination at API Gateway edge)

💡 Clarifying “HTTP API” Terminology Confusion
"HTTP API" in AWS ≠ All HTTP APIs

✅ Every API in API Gateway is HTTP-based

But AWS uses:

REST API → feature-rich, fine-grained control

HTTP API → optimized, minimal latency and cost

🧠 Think of HTTP API as:

“A streamlined version of REST API for modern, event-driven workloads”

🧪 Endpoint Differences (Visibly)
API Type	Example Endpoint
REST API	https://abc123.execute-api.us-east-1.amazonaws.com/dev/
HTTP API	https://xyz456.execute-api.us-east-1.amazonaws.com/

🧠 REST API includes stage in path
🧠 HTTP API doesn't require stages — simpler URLs

🔐 Auth Support Summary
Auth Type	REST API	HTTP API
IAM (SigV4)	✅ Yes	| ✅ Yes
Cognito (JWT)	✅ Yes	| ✅ Yes
JWT Authorizer	❌ No	| ✅ Yes
Lambda Authorizer	✅ Yes	| ✅ Yes
API Keys	✅ Yes	| ❌ No

🧠 TLS Termination: Both Support It
All API Gateway endpoints (REST or HTTP) are HTTPS only

TLS is terminated at API Gateway edge

No support for plain http://

✅ When to Use What (Architectural Perspective)
Use Case	API Type
Need Usage Plans, API Keys, WAF support	REST API
Building lightweight backend for SPA	HTTP API
Exposing public, low-latency Lambda API	HTTP API
Legacy enterprise app with fine-grained resource policies	REST API

📌 Exam Pointers
“Need lowest latency Lambda integration with OAuth2?” → ✅ HTTP API + Cognito

“Enforce usage plans per API key?” → ✅ REST API

“Need native CORS support for SPA?” → ✅ HTTP API

“API Gateway shows stage name in endpoint?” → ✅ REST API

“All API Gateway endpoints are HTTPS?” → ✅ Yes (TLS terminated)

🧠 TL;DR
Yes, all REST APIs are HTTP-based

AWS HTTP API ≠ REST architectural style — it’s a newer, simpler API Gateway product

✅ Both support TLS, auth, and HTTP methods

🧨 Choose REST API if you need legacy features, HTTP API for 90% of new workloads