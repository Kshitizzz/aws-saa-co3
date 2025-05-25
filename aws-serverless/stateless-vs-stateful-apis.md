# Stateless vs Stateful APIs – Deep Dive + Real Examples

## Memory Hook  
- “Stateless = every request is self-contained”  JWT based auth
- “Stateful = server remembers you between calls” Session cookies based auth WITH server / session stickiness (provided as a fatures in ELB)

---

## ✅ What Is a Stateless API?

> An API where **every request is independent** — it contains **all the information needed** to complete the request.

### 🔍 Characteristics
- ✅ No session or context stored on server
- ✅ Request has complete context (e.g., auth token, parameters)
- ✅ Easier to scale (no server affinity needed)
- ❌ Slightly more overhead per request (repeated context)

### ✅ Examples
- REST API
- AWS API Gateway + Lambda
- Amazon S3 API
- Any HTTP API that uses **JWT for stateless auth**

---

## 🧠 What Is a Stateful API?

> An API where the **server maintains context or session state** across multiple requests from the same client.

### 🔍 Characteristics
- Server “remembers” previous actions or state
- Session/token often stored on the server (e.g., in memory, DB, cache)
- ❌ Requires stickiness (client must talk to same backend instance)
- ✅ Useful when sequence of operations matters

### ✅ Examples
- WebSocket connections (long-lived session)
- SOAP with session tokens
- SSH, FTP, or Telnet-like protocols
- Traditional login-based apps with sticky sessions

---

## ✅ Is REST API Stateless?

Yes — it’s a **core constraint of REST**:

> "RESTful systems must be **stateless** — no session should be stored server-side between requests."

That’s why:
- Each REST request includes **all necessary context**
- Typically uses **HTTP headers** (e.g., `Authorization: Bearer <JWT>`)

---

## 🔁 Comparison Table

| Feature            | Stateless API                   | Stateful API                        |
|--------------------|----------------------------------|--------------------------------------|
| Server remembers?  | ❌ No                            | ✅ Yes                               |
| Scaling            | ✅ Easy (no session stickiness)  | ❌ Hard (requires affinity/session)  |
| Client context      | ✅ Sent in every request         | ❌ Shared via server-side state      |
| Reliability        | ✅ Easier to retry/failover      | ❌ Harder due to state dependency    |
| Examples           | REST, GraphQL, S3 API, Lambda   | WebSocket, SSH, SOAP w/ session      |

---

## 📌 Exam Pointers

- “What makes an API RESTful?” → ✅ Stateless, resource-based, cacheable
- “Which APIs are not stateless?” → ✅ WebSocket, SOAP (with session tokens)
- “Why is statelessness important in REST?” → ✅ It enables horizontal scaling and resilience
- “Does JWT make APIs stateless?” → ✅ Yes — all auth context is embedded in the token
