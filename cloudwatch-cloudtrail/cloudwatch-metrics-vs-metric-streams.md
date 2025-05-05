# CloudWatch Metrics vs Metric Streams

## Memory Hook
- “Metrics = Stored snapshots; Metric Streams = Live feed on steroids.”

---

## ✅ CloudWatch Metrics

### Must-Know Core Concepts
- Numeric data points from AWS services (e.g., CPUUtilization, Latency).
- Auto-collected every **1 or 5 minutes** depending on monitoring level:
  - Basic = 5-min granularity (free)
  - Detailed = 1-min granularity (paid)
- Visualized via:
  - CloudWatch Dashboards
  - Alarms
  - Logs Insights correlations
- Supports **custom metrics** via API or CW Agent.
- Metrics are kept for **15 months** (aggregation reduces over time):
  - 1-minute granularity → 15 days  
  - 5-minute granularity → 63 days  
  - 1-hour granularity → 15 months

### Exam Pointers
- “Monitor performance of EC2 or Lambda?” → ✅ CloudWatch Metrics
- “Want to alarm on high CPU?” → ✅ CloudWatch Metrics + Alarm
- “Granularity of metrics in free tier?” → ✅ 5 mins

---

## 🚀 CloudWatch Metric Streams

### Must-Know Core Concepts
- Real-time **push-based stream** of metric data to external systems.
- Sends metrics to:
  - **Amazon Kinesis Data Firehose**
  - 3rd party tools like **Datadog, Splunk** (via Firehose sink)
- Format: **OpenTelemetry 0.7 JSON** or **AWS format**.
- Useful for:
  - Centralized monitoring outside AWS
  - Low-latency ingestion into analytics platforms
- Near real-time (latency ~few seconds)

### Nuances & Edge Cases
- You **don’t see streamed data in CloudWatch console**.
- Doesn’t replace CloudWatch Metrics — it complements it.
- Has cost implications per **ingested metric datapoint per hour**.
- Requires setup of Firehose delivery stream.

### Exam Pointers
- “Send real-time metrics to Datadog or Splunk?” → ✅ Metric Streams
- “Want continuous monitoring outside AWS?” → ✅ Metric Streams + Firehose
- “Push-based real-time metric ingestion?” → ✅ Metric Streams

---

## 🔍 Summary

| Feature                  | CloudWatch Metrics         | Metric Streams                      |
|--------------------------|----------------------------|--------------------------------------|
| Purpose                  | Monitor & visualize in AWS | Push metrics to external tools      |
| Latency                  | 1–5 minutes                | Near real-time (~seconds)           |
| Integration              | Dashboards, Alarms         | Kinesis Firehose, 3rd party systems |
| Custom Metrics Support   | ✅ Yes                      | ✅ Yes (via stream)                  |
| Stored in AWS Console?   | ✅ Yes                      | ❌ No                                |
