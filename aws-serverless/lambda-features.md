# Deep Dive – AWS Lambda Features & Retry Behavior

## Memory Hook
- “Layers = shared code”
- “Provisioned = no cold starts”
- “Concurrency = don't blow up your backend”
- “Retry = async only retries automatically”

---

## ✅ 1. Lambda Layers

### What It Is  
- A way to package and share **common code/libraries** across multiple Lambda functions.

### Key Use Cases  
- Shared dependencies (e.g., NumPy, Pandas, logging packages)  
- App logic reuse across teams or services  
- Centralized library versioning

### Architecture  
- A layer is a **.zip file** uploaded to Lambda containing `/python` or `/nodejs` folder (or language-specific path)
- ✅ Up to 5 layers per function  
- ✅ Can share layers across accounts  
- ❌ Layers are immutable — new version = new upload

---

## ✅ 2. Concurrency Controls

| Control Type         | Description                                                      |
|----------------------|------------------------------------------------------------------|
| **Unreserved concurrency** | Lambda uses pool of available concurrency (shared)       |
| **Reserved concurrency**   | Function gets a guaranteed slice of concurrency (e.g. 50) |
| **Account-level concurrency** | Max concurrent executions across your account (default: 1,000) |

### Use Cases  
- Limit concurrency to **avoid backend overload**  
- Reserve concurrency to ensure **critical Lambda gets minimum resources**  
- Prevent a runaway function from **starving others**

### Example  
- You reserve 100 for `process-payment-fn`
- It can scale to 100 concurrent executions, even if others are throttled

---

## ✅ 3. Provisioned Concurrency

### What It Solves  
- **Cold start latency**, especially for:
  - VPC-connected Lambdas  
  - Heavy runtime functions (e.g., Java, .NET)  
  - APIs with strict SLAs

### How It Works  
- Lambda **keeps containers warm** in advance  
- You pay a **per-hour** + **per-invocation** fee for provisioned concurrency

### Use Cases  
- Customer-facing APIs (low latency)  
- Real-time processing (e.g., ML inference, chatbots)  
- Integrations with API Gateway HTTP APIs (or Function URLs)

---

## ⚠️ Provisioned vs Reserved

| Feature                  | Reserved Concurrency            | Provisioned Concurrency           |
|--------------------------|----------------------------------|-----------------------------------|
| Guarantees execution cap | ✅ Yes                          | ❌ No                             |
| Eliminates cold starts   | ❌ No (only limits invocations) | ✅ Yes (pre-warms containers)     |
| Use case                 | Protect downstream systems       | Minimize latency for cold starts |

---

## 🔁 Lambda Retry Mechanism

| Invocation Type   | Retry Behavior                                     |
|--------------------|----------------------------------------------------|
| **Synchronous (e.g., API Gateway)** | ❌ No automatic retry                 |
| **Asynchronous (e.g., S3, EventBridge)** | ✅ 2 retry attempts by default     |
| **Stream-based (DynamoDB, Kinesis)**     | ✅ Retries until **checkpoint succeeds** or item expires in stream

### Details

#### 🔸 Async Retry Logic
- Retry #1 = after a few seconds  
- Retry #2 = after a minute  
- If still fails:
  - ✅ Send to **DLQ** if configured (SQS/SNS)
  - ✅ Or to **Lambda Destination** (success/failure targets)

#### 🔸 Stream-Based Logic (DynamoDB/Kinesis)
- Lambda **keeps retrying until successful**
- Ordered processing → failure on one record = pause all records
- **Batch window, batch size, and max retry attempts** can be configured

---

## 📌 Exam Pointers

- “Want to avoid cold starts for an API endpoint?” → ✅ Use Provisioned Concurrency
- “Lambda failing async events?” → ✅ Use DLQ or Lambda Destinations
- “Need to share Pandas package across multiple Lambdas?” → ✅ Use Layers
- “DynamoDB stream processing is stuck on one record?” → ✅ Stream-based retry backoff
- “Prevent overloading a DB behind Lambda?” → ✅ Use Reserved Concurrency
