# Amazon Kinesis Data Stream vs Kinesis Data Firehose

## Memory Hook

- “Streams = Full control, Firehose = Fully managed”
- “Streams process, Firehose delivers”

---

## ✅ Kinesis Data Streams

### Must-Know Core Concepts

- Real-time streaming **data ingestion + processing pipeline**
- You can write custom **consumers** (like Lambda, EC2, KCL apps)
- Data stored in **shards** (parallelism units)
- Retention: 24 hrs (default) to 7 days
- Supports:
  - **Replay capability**
  - **Multiple consumers**
  - **Custom transformation logic**
- Good for:
  - Real-time analytics
  - Fraud detection
  - Log enrichment

---

## ✅ Kinesis Data Firehose

### Must-Know Core Concepts

- **Fully managed** delivery service for streaming data
- Supports **zero-code delivery** to:
  - S3
  - Redshift
  - Splunk
  - OpenSearch
- Can **transform data** via **Lambda** (optional)
- No data replay — **one-time flow**
- Buffering (size or time-based) before delivery
- Fully auto-scaling — no shards to manage

---

## 🧠 Key Differences

| Feature                  | Kinesis Data Streams            | Kinesis Firehose                    |
|--------------------------|----------------------------------|-------------------------------------|
| Management               | Manual (shards, consumers)       | Fully managed                        |
| Processing               | You build consumers              | AWS delivers to destination         |
| Replay / Reprocessing    | ✅ Yes (within retention window)  | ❌ No                                |
| Destinations             | Anything (via consumer logic)    | S3, Redshift, OpenSearch, Splunk    |
| Transformation           | ✅ You handle it                  | ✅ Optional via Lambda               |
| Use Case                 | Real-time logic & branching      | Simple delivery to storage/analytics |
| Scaling                  | You manage shards                | Auto-scaled                         |

---

## 📌 Exam Pointers

- “Need to store logs into S3 without coding?” → ✅ Firehose
- “Custom app wants to read & process data stream?” → ✅ Data Stream
- “Want to replay log data or attach multiple consumers?” → ✅ Data Stream
- “Push VPC Flow Logs to S3?” → ✅ Firehose
- “Real-time fraud detection system?” → ✅ Data Stream + Lambda

---

Let me know if you want:
- Diagram of Kinesis integrated with CloudWatch Logs
- Or we resume with CloudTrail (audit logging)
