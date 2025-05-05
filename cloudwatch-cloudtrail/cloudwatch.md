# Amazon CloudWatch

## Memory Hook
- “CloudWatch = Your Cloud Ka FitBit”
- “Monitor. Alarm. Visualize. Trigger. All from one place.”

---

## ✅ Must-Know Core Concepts

- **Monitoring & observability** service for AWS resources and custom apps.
- Core capabilities:
  - 📊 **Metrics**: Auto-collected (CPU, latency, disk, etc.)
  - 📜 **Logs**: Store and query logs from Lambda, EC2, API Gateway, etc.
  - ⏰ **Alarms**: Trigger when metrics cross a threshold
  - 🖼️ **Dashboards**: Visualize metrics in real time
  - ⚙️ **Events (EventBridge)**: Route events to actions (e.g., run Lambda on alarm)
- Supports **custom metrics** from on-prem or external apps via API.
- Alarms can trigger:
  - SNS alerts
  - Auto Scaling actions
  - Lambda functions
- **Retention**: Metrics retained for 15 months (granularity decreases over time).

---

## ⚠️ Nuances & Edge Cases

- **Basic monitoring**: 5-minute granularity  
  **Detailed monitoring**: 1-minute granularity (requires enabling, extra cost).
- For EC2 memory/disk metrics → Need to install **CloudWatch Agent**.
- Can **log data from on-prem servers** too.
- Alarms don’t work on logs directly — you must use **CloudWatch Logs + Metric Filters**.
- **Log retention** must be explicitly configured — defaults to “never expire”.

---

## 🧠 Exam Pointers

- “Trigger Lambda when CPU > 80%?” → ✅ CloudWatch Alarm + EventBridge
- “Want to visualize service health in a dashboard?” → ✅ CloudWatch
- “Need metrics for Lambda execution time?” → ✅ CloudWatch Metrics
- “Want to alert on ‘error’ string in log?” → ✅ CloudWatch Logs + Metric Filter + Alarm
- “Auto-scale based on average CPU”? → ✅ CloudWatch + Auto Scaling Group

---

## 🧩 Related Components

- **CloudWatch Logs** → Stores raw logs from services
- **CloudWatch Agent** → Required for memory/disk metrics on EC2
- **CloudWatch Logs Insights** → Log query engine (SQL-like)
- **EventBridge (formerly CloudWatch Events)** → Rule-based routing of events
