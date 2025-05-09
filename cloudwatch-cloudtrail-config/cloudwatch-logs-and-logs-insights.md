# CloudWatch Logs & Logs Insights

## Memory Hook

- “Logs = What happened? Insights = Why it happened?”
- “One place to collect, search, and alert on all your logs.”

---

## ✅ CloudWatch Logs

### Must-Know Core Concepts

- **Centralized log storage** service for AWS resources & custom apps.
- Logs are stored in **Log Groups** → each has **Log Streams** (per source).
- Integrated with:
  - Lambda (invocation logs)
  - API Gateway (access logs)
  - EC2 (via CloudWatch Agent)
  - ECS, Fargate, Step Functions, etc.
- Logs can be:
  - Searched manually
  - Filtered using **Metric Filters**
  - Archived to S3
  - Streamed to Kinesis/Data Lakes

### Nuances & Edge Cases

- **Retention is NOT set by default** → must configure to avoid extra costs.
- Log Group name is important for organizing environments (`/aws/lambda/<func-name>` etc.)
- Alarms cannot be set directly on logs → need **metric filters** to extract data first.
- **CloudWatch Agent** required for EC2 system logs (memory, disk, custom app logs).

---

## 🧪 Metric Filters (Important Exam Detail)

- Define a **pattern to match inside logs** (e.g., `"ERROR"` or `status=500`).
- Converts matches into a **CloudWatch Metric**.
- Then you can trigger:
  - Alarms
  - SNS notifications
  - Lambda remediation

**Exam Hook:**  
> “Want to trigger an alarm when log has 'Unauthorized'?”  
✅ Use Metric Filter → CloudWatch Metric → Alarm

---

## 🔍 CloudWatch Logs Insights

### Must-Know Core Concepts

- **Interactive query tool** to explore and analyze logs using SQL-like syntax.
- Fast, serverless, scalable — works directly on CloudWatch Logs.
- Common operations:
  - `filter` → search logs
  - `stats` → aggregation (count, avg, percentiles)
  - `parse` → extract fields
  - `sort`, `limit`, `fields` → formatting

### Sample Query

```sql
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
