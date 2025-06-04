# Amazon SQS – Deep Dive (AWS SAA-C03)

## 🧠 Memory Hook

- “**SQS = Buffer Zone** between microservices.”
- “**Don’t drop the message, queue it.** Decouple like a pro.”
- Temporary parking lot for messages between producers and consumers.

---

## 🔑 Must-Know Core Concepts

- Fully managed message queuing service to **decouple** services.
- Guarantees **loose coupling**, **scalability**, and **fault tolerance**.
- Integrates with: **EC2, Lambda, ECS, S3, API Gateway, SNS, CloudWatch**, etc.

### Queue Types:

| Queue Type        | Behavior                                      |
|-------------------|-----------------------------------------------|
| Standard Queue    | **At-least-once**, **Best effort ordering**, unordered, high throughput |
| FIFO Queue        | **Exactly-once**, **ordered**, limited throughput |
| DLQ (Dead Letter) | For failed messages after retry attempts      |

---

## 🧱 Real-World Usage Patterns

- **Decouple Microservices**: API Gateway or Lambda sends messages → EC2/Lambda pulls.
- **Auto Scaling Workers**: ASG scales EC2 consumers based on CloudWatch queue depth metrics and alarm.
- **Fan-Out with SNS**: SNS topic sends same message to multiple SQS queues.
- **Buffering Writes**: Buffer bursts before writing to RDS or DynamoDB, like in Kinesis Data Firehose
- **Reprocessing Support**: Re-read messages for audits or retries, also fault tolerant
- **S3 Event Trigger**: Object created → message sent to SQS → triggers further processing through lambda (eg)

---

## ⚙️ Feature Summary

| Feature                 | Value                                         |
|-------------------------|-----------------------------------------------|
| Retention               | 1 min – 14 days (default: 4 days)             |
| Visibility Timeout      | 0 – 12 hours (default: 30 sec)                |
| Max Message Size        | 256 KB                                        |
| Delay Queues            | Delay messages for up to 15 minutes  (time.sleep())         |
| Long Polling            | Avoids empty responses, saves cost            |
| DLQ                     | Captures failed messages for diagnostics      |
| Encryption              | SSE-KMS (at rest), TLS (in transit)           |
| Throughput (FIFO)       | 300 msg/sec (or 3,000 with batching)          |

---

## ⚠️ Nuances & Edge Cases

- **FIFO queues** require `MessageGroupId` to maintain order.
- **Standard queues** may deliver duplicates; idempotency is required.
- **Long polling** saves API cost, avoids hot-loop polling.
- **DLQs** don’t process, only store for debugging.
- Consumers must **explicitly delete messages** after successful processing.

---

## 📘 Exam Pointers

- Use **Standard Queues** for scale; **FIFO Queues** for ordering.
- DLQs handle poison messages after retry limit is reached.
- IAM policies needed for send/receive/delete access.
- SQS doesn’t push → **consumers poll** for messages.
- Use CloudWatch alarms on `ApproximateNumberOfMessages` for **auto scaling**.

---

## 🔌 Service Integrations

| AWS Service     | Integration Example                                        |
|-----------------|------------------------------------------------------------|
| Lambda          | Polls SQS for serverless processing                        |
| EC2             | Batch workers pull messages                                |
| S3              | Sends object-created events to SQS                         |
| API Gateway     | Sends message to SQS directly (async flow)                 |
| SNS             | SNS → SQS fan-out pattern                                  |
| Step Functions  | Uses SQS for wait states or step decoupling                |
| ECS/Fargate     | Tasks pull messages as jobs                                |

---

## 💡 System Design Use Cases

- **Traffic spike buffering**
- **Retry management with DLQs**
- **Decoupled data processing pipelines**
- **Autoscaling workers based on queue depth**
- **Fan-out for parallel processing**

---

## 💀 Anti-Patterns

- Don’t treat SQS as a **database**.
- Avoid long message retention for stateful logic.
- Be cautious of **zombie messages** due to improper visibility timeout.

---
