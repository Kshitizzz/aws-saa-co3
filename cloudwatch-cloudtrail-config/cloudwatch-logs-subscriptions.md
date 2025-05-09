# CloudWatch Logs Streaming & Subscriptions

## Memory Hook

- "Logs go live, filter to fire."
- "From Logs to Lambda/Firehose — analytics without delay."

---

## ✅ Must-Know Core Concepts

### 📌 CloudWatch Logs Subscriptions

- **Push-based streaming mechanism** to forward log events in near real-time.
- You apply a **Subscription Filter** to a Log Group:
  - Filter pattern (e.g., “ERROR”)
  - Destination:
    - **Lambda Function**
    - **Kinesis Data Stream**
    - **Kinesis Data Firehose**
    - **Cross-account destination**

- Delivers logs in real time **as they arrive** in the log group.

---

### 🔀 Use Cases

| Destination       | Common Use Case                                    |
|-------------------|----------------------------------------------------|
| Lambda            | Real-time parsing, alerting, anomaly detection     |
| Kinesis Data Stream | Buffering for analytics, custom dashboards         |
| Kinesis Firehose  | Real-time delivery to **S3, Redshift, Splunk**     |
| Cross-Account     | Aggregating logs from multiple AWS accounts        |

---

## 🔁 Cross-Account Log Aggregation

- Use a **destination Log Group in central account**.
- Use **AWS::Logs::Destination** + **resource policy** to allow other accounts.
- The sender account **creates a subscription filter**, targeting this **cross-account destination ARN**.

🧠 **Use case:** Multi-account setups with centralized logging in security/compliance accounts.

---

## 🚀 Real-Time Log Export Pipelines

| Pipeline                | Description                                                 |
|-------------------------|-------------------------------------------------------------|
| Logs → Lambda           | Real-time trigger-based analytics (e.g., send alerts to Slack) |
| Logs → Kinesis Stream   | Feed to analytics engine / stateful app                     |
| Logs → Kinesis Firehose | Send to S3/Redshift/Splunk for indexing                     |
| Logs → S3               | Long-term storage (batch or stream via Firehose)            |

---

## 📦 Batch Export to S3

- Use **Export Tasks** from CloudWatch Logs console or API.
- Only supports logs stored in **Log Groups**, **NOT real-time**.
- Common for:
  - Archival
  - Offline compliance
  - Legacy analysis tools

🧠 This is **pull-based** and **not real-time** — suitable for weekly/monthly exports.

---

## ⚠️ Nuances & Edge Cases

- **Subscription Filters are per log group**, not per log stream.
- Subscriptions **can only be one per log group**.
- Cross-account subscriptions require **resource policy on destination ARN**.
- Kinesis Data Stream gives more **processing control** (e.g., replay, batch).
- Kinesis Firehose is **fully managed**, no replay, good for simple pipelines.
- **Lambda payload limit = 256 KB** — ensure log payload fits.

---

## 📌 Exam Pointers

- “Real-time log processing → Lambda or analytics engine?” → ✅ Logs Subscription + Lambda or Kinesis
- “Send logs from dev/test/prod to central SIEM?” → ✅ Cross-account Logs Subscriptions
- “Archive logs daily to S3?” → ✅ Batch Export or Firehose
- “Want log transformation before storage?” → ✅ Logs → Lambda → S3/Firehose
- “Build custom alerting engine on logs?” → ✅ Logs → Kinesis Stream → Custom Analytics

