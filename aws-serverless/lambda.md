# AWS Lambda – SAA-C03 Prep Guide

## Memory Hook  

- “Zero servers. Infinite scale. Pay for what you run.”

---

## ✅ What Is AWS Lambda?

- **Serverless compute service** that runs your code in response to **events**
- No server provisioning or management
- Code runs inside **isolated containers** managed by AWS
- Billed by **invocation count + execution time (ms)**

---

## ✅ Core Concepts

| Concept              | Details                                                    |
|----------------------|------------------------------------------------------------|
| **Trigger-based**     | Invoked via API Gateway, S3, DynamoDB, EventBridge, etc.  |
| **Ephemeral compute** | Container runs temporarily, auto-scales                   |
| **Stateless**         | No state between invocations unless you use external store (e.g., S3, DynamoDB) |
| **Concurrency**       | Scales by running multiple containers simultaneously       |
| **Timeout**           | Max 15 minutes per execution                              |

---

## 🧠 Lambda Execution Model

1. Event triggers function
2. AWS provisions (or reuses) a container
3. Your code executes with:
   - Memory: 128 MB to 10 GB
   - CPU allocated proportionally
4. Logs go to **CloudWatch Logs**

---

## ✅ Key Features to Remember

| Feature                  | Description                                               |
|--------------------------|-----------------------------------------------------------|
| **Function URL**         | Built-in HTTPS endpoint (no API Gateway needed)           |
| **Environment variables**| Secure key-value store inside function config             |
| **Dead Letter Queue (DLQ)** | Capture failed async events to SQS/SNS                 |
| **Lambda Destinations**  | Route success/failure of async invocation to another Lambda, SNS, SQS, EventBridge |
| **Layers**               | Reusable libraries, shared across functions               |
| **Concurrency controls** | Limit concurrent executions (per function or globally)    |
| **Provisioned concurrency** | Pre-warm containers to reduce cold starts              |
| **VPC integration**      | Access RDS, ElastiCache, etc. inside private subnets      |

---

## 📦 Supported Runtimes

- Node.js, Python, Java, Go, Ruby, .NET, and **custom runtimes via container images**
- Also supports **Graviton2** (ARM) for cost-effective compute

---

## 🔄 Triggering Sources (Integrated Services)

| Trigger Source         | Use Case Example                        |
|------------------------|------------------------------------------|
| **API Gateway**         | REST/HTTP APIs                          |
| **S3**                  | Object upload triggers                  |
| **DynamoDB Streams**    | Change detection                        |
| **SQS**                 | Message queue processing                |
| **EventBridge**         | Event-driven workflows                  |
| **CloudWatch Logs**     | Log processing                          |
| **CloudFormation**      | Custom resource handlers                |

---

## 💸 Pricing Breakdown

- **Requests**: First 1M/month free, then $0.20 per million
- **Compute**: Pay per ms of execution + memory allocated
- **Extra cost for**:
  - VPC ENIs (setup latency + cost)
  - Provisioned concurrency
  - Function URLs if over quota

---

## ⚠️ Gotchas & Limits

- Max timeout: 900 seconds (15 minutes)
- Max size of zipped deployment: 50 MB (direct), 250 MB (via S3)
- **No built-in retry** for sync invocations
- **Async invocations retry 2x by default**, then to DLQ (if configured)
- Event payload size limits vary (e.g., API Gateway: 6 MB max for proxy integration)

---

## 📌 Exam Pointers

- “Need to execute code on S3 file upload?” → ✅ Lambda trigger on S3 event
- “Need low-latency, HTTPS endpoint with minimal setup?” → ✅ Lambda Function URL
- “Handle unpredictable workload spikes?” → ✅ Lambda auto-scales with demand
- “Prevent cold starts?” → ✅ Use Provisioned Concurrency
- “Log and monitor Lambda performance?” → ✅ Use CloudWatch Logs + CloudWatch Metrics
- “Need retry logic on failure?” → ✅ Use DLQ or Destinations for async flows
