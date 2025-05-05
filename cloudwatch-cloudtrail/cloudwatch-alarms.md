# Amazon CloudWatch Alarms

## Memory Hook

- “Metric + Threshold = Alarm Action”
- “Alarm = Trigger on condition breach, Act in real time”

---

## ✅ Must-Know Core Concepts

- Used to **monitor CloudWatch Metrics** and respond to changes.
- States:
  - `OK`: Metric is within the threshold
  - `ALARM`: Threshold is breached
  - `INSUFFICIENT_DATA`: Not enough data to evaluate
- Supports **Static** and **Anomaly Detection** thresholds.
- Can trigger:
  - **SNS notifications** (email, SMS, Slack via Lambda)
  - **Auto Scaling Policies**
  - **Lambda functions**
  - **EC2 recovery actions**
  - **Systems Manager Automation**
  - **EventBridge rules**
- Based on:
  - Single metric or composite (multi-metric) alarm
  - Period, datapoints evaluation (e.g., "3 out of 5")

---

## 🧪 Alarm Types

| Type                  | Description                                       |
|-----------------------|---------------------------------------------------|
| **Standard Alarm**    | Triggered on a single metric (e.g., CPU > 80%)   |
| **Composite Alarm**   | Combines multiple alarms (e.g., A OR B triggers) |
| **Anomaly Detection** | Uses ML to detect deviations from normal metric  |

---

## ⚙️ Key Parameters

- **Metric Name** (e.g., `CPUUtilization`)
- **Period** (e.g., every 60 seconds)
- **Evaluation Periods** (e.g., 3 of last 5)
- **Threshold Type**:
  - Static (e.g., > 80%)
  - Anomaly detection band (dynamic)

🧠 *Example:*  
"CPU > 80% for 3 consecutive periods of 1 minute each" → Alarm triggers

---

## ⚠️ Nuances & Edge Cases

- **Only 1 action per state** — OK, ALARM, INSUFFICIENT_DATA
- Use **composite alarms** for complex scenarios (e.g., AND, OR logic)
- **Alarms don’t persist data** — they evaluate metrics in real-time
- **SNS topic must have subscription** to notify users
- Alarms on **custom metrics** cost extra if not in free tier
- You can suppress alarms during planned maintenance using **Alarm suppression rules**

---

## 📌 Exam Pointers

- “Trigger Lambda when error count > 10” → ✅ Alarm on `Error` metric
- “Scale EC2 fleet based on CPU usage” → ✅ Alarm → Auto Scaling Policy
- “Avoid false alarms due to jittery metrics” → ✅ Use `N out of M` evaluation periods
- “Detect performance anomaly” → ✅ Use **Anomaly Detection Alarm**
- “Combine conditions from multiple metrics” → ✅ Use **Composite Alarm**

---

## 🔁 Alarm Actions in Real Architectures

| Trigger Condition              | Alarm Action                     |
|-------------------------------|----------------------------------|
| CPU > 80%                     | Launch new EC2 via Auto Scaling |
| Lambda errors > threshold     | Send alert via SNS              |
| RDS storage usage ↑           | Invoke SSM to clean temp files  |
| System status check fail      | Recover EC2 automatically       |

---

## 🧠 Extra: Common Alarm Use Cases

- Monitor S3 bucket size growth
- Alert on failed login attempts (via logs + metric filters)
- Detect increased latency in API Gateway
- Notify on expired TLS certs or secrets

