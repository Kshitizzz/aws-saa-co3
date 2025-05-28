# API Communication Protocols – REST, SOAP, GraphQL, gRPC, and Beyond

## Memory Hook  
- “APIs speak many languages — choose the one that speaks best for your use case.”

---

## ✅ 1. REST (Representational State Transfer)

> **Architectural style** built on HTTP — not a strict protocol

- Stateless, resource-based, cacheable
- Uses HTTP verbs (GET, POST, PUT, DELETE)
- JSON or XML as payload (mostly JSON now)

✅ Widely used in web/mobile APIs  
✅ Simple, language-agnostic  
❌ No strong typing, versioning is messy

---

## ✅ 2. SOAP (Simple Object Access Protocol)

> Strict, **XML-based protocol** with WSDL and strong schema

- State-aware via session headers
- Supports ACID transactions, security (WS-Security), and contracts
- Communicates over HTTP, SMTP, etc.

✅ Used in enterprise systems, banks, healthcare  
✅ Excellent tooling in Java/.NET ecosystems  
❌ Verbose, complex, slower than REST

---

## ✅ 3. GraphQL (Query Language for APIs)

> Flexible **client-driven query protocol** built over HTTP

- Clients specify what data they want (no over-fetching)
- Single endpoint replaces many REST endpoints
- Uses **schema + typed queries**

✅ Great for frontends (React, mobile apps)  
✅ Solves REST under/over-fetching  
❌ Complex caching, security, rate-limiting

---

## ✅ 4. gRPC (Google Remote Procedure Call)

> **Binary RPC protocol** using HTTP/2 + Protocol Buffers

- Strongly typed, fast, bi-directional streaming
- Contracts defined via `.proto` files
- High performance, low latency

✅ Ideal for internal microservice-to-microservice calls  
✅ Used in Kubernetes, Envoy, CNCF stack  
❌ Not browser-friendly, hard to debug over wire

---

## ✅ 5. WebSocket

> Bi-directional, full-duplex communication over a single TCP connection

- State is maintained across connection
- Not RESTful — lives outside HTTP once handshake completes

✅ Great for chat apps, real-time dashboards  
✅ Used in multiplayer games, live feeds  
❌ Requires connection management

---

## ✅ 6. Server-Sent Events (SSE)

> Unidirectional stream from server to client over HTTP

- Client subscribes → server pushes updates
- Simpler than WebSockets for streaming

✅ Good for real-time notifications, logs  
❌ One-way only (server → client)

---

## ✅ 7. Webhooks

> Not a protocol but a **push-based pattern** using HTTP POST

- App A sends data to App B when an event occurs

✅ Used in Stripe, GitHub, Slack integrations  
❌ No delivery guarantee unless retried manually

---

## ✅ 8. JSON-RPC / XML-RPC

> Minimalist **remote procedure call protocols** using JSON or XML

- Client sends method name + parameters  
- Server returns result or error

✅ Simpler than SOAP  
❌ No type enforcement, versioning

---

## ✅ 9. AMQP / MQTT / STOMP (Messaging APIs)

> Protocols used for **message brokers and pub/sub systems**

- Not request/response — event-driven
- Used with RabbitMQ, ActiveMQ, AWS IoT, etc.

✅ Ideal for IoT, event buses, background processing  
❌ Not HTTP, requires broker setup

---

## ✅ Comparison Summary

| Protocol       | Format     | Strengths                             | Used In                                 |
|----------------|------------|----------------------------------------|------------------------------------------|
| REST           | HTTP + JSON | Simple, widely supported               | Web, mobile, server APIs                 |
| SOAP           | HTTP + XML  | Rigid, secure, contract-first          | Banks, government, legacy systems       |
| GraphQL        | HTTP + JSON | Flexible, typed, client-driven         | SPAs, React, mobile APIs                 |
| gRPC           | HTTP/2 + Protobuf | Fast, strongly typed, streaming    | Internal microservices, gCloud, K8s     |
| WebSocket      | TCP        | Bi-directional, low latency            | Chat, games, trading apps               |
| SSE            | HTTP       | One-way server push                    | Alerts, logs, streaming dashboards      |
| Webhooks       | HTTP POST  | Event-driven triggers                  | SaaS integrations (Slack, Stripe)       |
| JSON-RPC       | HTTP + JSON | Minimal RPC                            | Lightweight client-server APIs          |
| MQTT/AMQP      | Binary     | Pub/sub messaging                      | IoT, message queues                      |

---

## 📌 Exam & Real-World Pointers

- “Build a flexible, client-driven API?” → ✅ Use GraphQL  
- “Real-time stock feed dashboard?” → ✅ WebSockets or SSE  
- “Need secure, verifiable B2B contract-based API?” → ✅ SOAP  
- “Internal microservices with high throughput?” → ✅ gRPC  
- “Need to notify 3rd party when order is placed?” → ✅ Webhook  
- “IoT sensors publish telemetry data?” → ✅ MQTT

