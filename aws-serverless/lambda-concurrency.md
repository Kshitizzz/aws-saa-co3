# AWS Lambda Concurrency, Cold Starts & Throttling – Deep Dive

## Memory Hook  
- “Reserved = guaranteed seats”  
- “Provisioned = pre-warmed engines”  
- “Unreserved = may get throttled”  
- “Cold start = the engine’s off, and you called an Uber”

---

## ✅ What Is Lambda Concurrency?

> Concurrency = the number of Lambda function instances running **at the same time**

- If 5 events arrive at the same time → 5 concurrent executions
- AWS automatically scales by spinning up containers for each concurrent invocation

---

## ❄️ What Are Cold Starts?

- When a **new Lambda container** spins up:
  - Initializes runtime + imports
  - Runs handler

🧠 Only the **first request per container** is affected  
- Typically adds **100ms to 1s** delay
- Affects **performance-sensitive, low-latency** apps (e.g., APIs)

---

## 🔁 Lambda Scaling Behavior

| Behavior                  | Default |
|---------------------------|---------|
| **Initial burst**         | 500–3000 concurrency (region-dependent)  
| **Steady scaling**        | +500 invocations/minute  
| **Account concurrency quota** | 1,000 (soft limit; raiseable)  
| **When exceeded?**        | 🔥 Lambda is throttled

---

## 💥 What Is Throttling?

> AWS **rejects/delays** invocations when no concurrency is available

- **Synchronous** (API Gateway): returns HTTP `429 TooManyRequests`
- **Asynchronous** (S3, EventBridge): retries 2x, then goes to DLQ (if configured)
- **Stream-based (Kinesis/DDB)**: retries until success or data expires

🧠 Throttling = **invocation drops due to lack of available capacity**

---

## ✅ Reserved Concurrency

> Dedicated concurrency quota **for a specific Lambda function**

| Behavior                   | Result                        |
|----------------------------|-------------------------------|
| Sets **maximum concurrency** | Caps function scale-out      |
| Guarantees minimum         | Prevents starvation by others |
| Removes from shared pool   | ✅ Isolated from rest          |

🧠 Good for:
- Protecting production functions
- Throttling dev/test functions intentionally

---

## ✅ Provisioned Concurrency

> Pre-warms containers so function is **instantly ready** → eliminates cold starts

| Behavior                       | Result                                |
|-------------------------------|----------------------------------------|
| Containers **always warmed**   | ✅ No cold starts                      |
| ✅ Pay for idle time           | Per-hour + per-request cost            |
| Can be combined with reserved | For guaranteed warm & isolated runs    |

🧠 Best for:
- REST APIs, ML inference, chatbots
- Any latency-sensitive use case


## 📌 Exam Pointers

- “Cold starts hurting latency?” → ✅ Use Provisioned Concurrency
- “Prevent one Lambda from starving others?” → ✅ Use Reserved Concurrency
- “Lambda returning 429 errors?” → ✅ You’re being throttled
- “Async events not processed?” → ✅ DLQ or Destinations needed
- “Stream stuck on one record?” → ✅ It’s retrying until that record succeeds

