# Amazon SQS – Core Features Deep Dive

---

## 🧠 Memory Hook

- "SQS = Inbox for distributed systems."
- "Send → Queue → Receive → Delete. That’s the lifecycle."

---

## 🚀 Must-Know Core Concepts

### 🕐 Message Visibility Timeout

- Temporarily hides the message after a consumer picks it up.
- Prevents multiple consumers from processing the same message.
- **Default**: 30 seconds. **Configurable**: 0 to 12 hours.
- If not deleted in time, message becomes visible again.
- Leads to **at-least-once delivery**.

> ✅ **Example**:  
> A Lambda function processing a video takes 10s.  
> Set visibility timeout to 20s to prevent premature retry.

---

### 📬 Long Polling

- Waits for a message to arrive instead of returning empty.
- Saves cost by reducing **empty receives** and API calls.
- Max wait time: **20 seconds**.
- Improves efficiency and reduces CPU utilization.

> ✅ **Example**:  
> Polling every second burns money. Use long polling with `WaitTimeSeconds=20`.

---

### ☠️ Dead-Letter Queue (DLQ)

- A **backup queue** for messages that fail processing repeatedly.
- Used to isolate and debug problematic messages.
- Configure with **redrive policy** (maxReceiveCount threshold).

> ✅ **Example**:  
> Image resize fails 5 times → message lands in DLQ for later analysis.

---

### ⏳ Message Retention Period

- How long a message stays in the queue if not deleted.
- **Default**: 4 days. **Range**: 60 seconds – 14 days.
- After expiry, messages are deleted automatically.

---

### 🧪 FIFO Message Deduplication

- FIFO queues support **exactly-once processing**.
- Two types:
  - `MessageDeduplicationId` (explicit)
  - `ContentBasedDeduplication` (AWS-generated hash of message body)

> ✅ **Example**:  
> Avoid duplicate orders in e-commerce checkout with FIFO + deduplication.

---

### 🪢 Message Group ID (FIFO Queues)

- Maintains strict **message ordering** for same group ID.
- One consumer at a time per group.
- No ordering guarantee across different groups.

---

### 🔁 Delay Queues

- Delays delivery of a message to the queue.
- Configurable per-message or queue-wide.
- Helps implement retry-with-backoff patterns.

> ✅ **Example**:  
> Retry failed tasks with exponential backoff using message delay.

---

## ⚠️ Nuances & Edge Cases

- **Visibility timeout ≠ retention period**.
- Must configure **long polling at both queue & API level**.
- DLQs don’t activate automatically — must **opt-in** and configure.
- Max message size = **256 KB**. For larger payloads → store in **S3**, pass reference via SQS.
- Standard queue = **at-least-once**, so idempotent consumers are required.

---

## ✅ Exam Pointers

- FIFO + Message Group ID = **ordered** processing.
- Standard queue = **higher throughput**, less strict ordering.
- DLQ helps **debug poison messages**.
- Visibility timeout errors can cause **duplicate processing**.
- Long polling is **cheaper + better** than short polling.
- DLQs must be **separately configured**, not automatic.

---

## 🛠 Real-World Integrations

- **ASGs** can push failed jobs or batch tasks to SQS.
- **Lambda triggers** directly from SQS — ensure batch size and visibility are tuned.
- Use **S3 + SQS** to process large files asynchronously.

---

Let me know if you want to move on to:
- **Lambda + SQS flow**
- **Redrive Policy implementation**
- **SQS vs SNS vs Kinesis**
