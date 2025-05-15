# AWS CloudTrail

## Memory Hook
- “Who did *what*, *when*, *where*, and *how* — CloudTrail knows.”
- “CloudTrail = API activity logger for your entire AWS account.”

---

## ✅ Must-Know Core Concepts

- CloudTrail **records API calls** made to AWS services:
  - Via AWS Console
  - AWS CLI
  - SDKs
  - AWS services on your behalf (e.g., Lambda, Auto Scaling)
- Events include:
  - `who` (IAM identity)
  - `what` (API called)
  - `when` (timestamp)
  - `where` (source IP, region)
  - `request` + `response` metadata

---

### 🎯 Event Types

| Type             | Description                                     |
|------------------|-------------------------------------------------|
| **Management Events** | Control-plane actions (e.g., CreateBucket, StopInstance) |
| **Data Events**       | Data-plane actions (e.g., GetObject from S3, PutItem in DynamoDB) |
| **Insights Events**   | Detect unusual API activity (e.g., spikes in write actions) |

🧠 *Data Events must be explicitly enabled — not logged by default.*

---

## 🗂️ Trail Configuration

- **Single Region vs Multi-Region**:
  - By default, logs **all regions**
- **Create a Trail** to:
  - Send logs to **S3**
  - Send logs to **CloudWatch Logs** (for alerting/monitoring)
- **Organizational Trail**: Logs activity across all accounts in AWS Org

---

## 🧪 Use Cases

- Forensics (after a security breach)
- Compliance (PCI, HIPAA, etc.)
- User activity tracking
- Alerting on sensitive actions (via EventBridge + CloudWatch)

---

## ⚠️ Nuances & Edge Cases

- **First copy of management events is free**  
- **Data events (e.g., S3 object access)** incur extra charges
- Trails can be **global**, even if service is regional
- **Log file integrity validation** supported using hash digest files
- Doesn’t record all “read-only” API calls — some very low-level calls might not be captured

---

## 📌 Exam Pointers

- “Need to track who deleted an S3 bucket?” → ✅ CloudTrail
- “Centralized audit log for all Org accounts?” → ✅ Org Trail
- “Detect sudden surge in DynamoDB writes?” → ✅ CloudTrail Insights
- “Need forensic history of API calls?” → ✅ CloudTrail
- “Want to alert on certain API activity?” → ✅ CloudTrail → EventBridge Rule → Alarm/Lambda

---

## 🔄 CloudTrail vs Other Servicess

| Service        | What it Logs                         | Use Case                                  |
|----------------|---------------------------------------|-------------------------------------------|
| **CloudTrail** | API calls & identity info             | Auditing, compliance                      |
| **CloudWatch Logs** | App/system logs, metrics            | Debugging, monitoring                     |
| **AWS Config** | Resource config changes               | Compliance, configuration drift detection |
