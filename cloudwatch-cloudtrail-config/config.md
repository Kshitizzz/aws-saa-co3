# AWS Config

## Memory Hook

- “AWS Config = Git for your Cloud Resources.”
- “Track config changes + enforce compliance.”

---

## ✅ Must-Know Core Concepts

- Tracks **configuration changes** to supported AWS resources (e.g., EC2, S3, Security Groups).
- Stores a **history of all config states** per resource (like snapshots).
- Can evaluate changes **against compliance rules**.
- Supports:
  - **Managed Rules** (prebuilt AWS rules)
  - **Custom Rules** (via Lambda functions)
- Records:
  - Resource relationships (e.g., EC2 attached to SG)
  - Before/After config snapshots
  - Change time + triggering API (via CloudTrail integration)

---

## 🧪 Use Cases

- Detect **non-compliant resources** (e.g., public S3 buckets)
- Automate **remediation** (via Config + SSM or Lambda)
- Visualize **resource drift** over time
- Generate **compliance reports** for audits (PCI, HIPAA, etc.)

---

## 🧩 Core Components

| Component       | Description                                           |
|------------------|-------------------------------------------------------|
| **Configuration Recorder** | Captures config changes (1 per region/account)      |
| **Delivery Channel**        | Where AWS Config stores data (usually S3)         |
| **Rules**                   | Define compliance logic                          |
| **Remediation**             | Optional automation to fix non-compliant state   |

---

## 📌 Exam Pointers

- “Detect and auto-remediate non-compliant SG rules?” → ✅ AWS Config + Rule + Remediation
- “Audit historical config of S3 bucket versioning?” → ✅ AWS Config Timeline
- “Evaluate compliance against CIS Benchmarks?” → ✅ AWS Config Managed Rules
- “Track relationships between VPC components?” → ✅ AWS Config Resource Graph
- “Receive compliance status updates?” → ✅ EventBridge or SNS integration

---

## ⚠️ Nuances & Edge Cases

- **Not all AWS resources are supported** (check the [AWS Config supported list](https://docs.aws.amazon.com/config/latest/developerguide/resource-config-reference.html))
- Must be **enabled per region/account**
- **Charges apply per configuration item recorded**
- **Rules only evaluate when triggered by change or periodically**
- Integrates **natively with CloudTrail, S3, and Lambda**

---

## 🔄 AWS Config vs CloudTrail vs CloudWatch

| Feature       | CloudTrail              | Config                      | CloudWatch                    |
|----------------|--------------------------|------------------------------|-------------------------------|
| **What**       | API calls                | Resource state/config       | Logs, metrics, alarms         |
| **When**       | Real-time event stream   | Periodic + change-triggered | Continuous monitoring         |
| **Why**        | Audit, who did what      | Compliance, config drift    | Operational visibility        |

