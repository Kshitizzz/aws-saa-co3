# AWS Security: GuardDuty vs Inspector vs Macie

## Memory Hook

- "GuardDuty = Threat Detection Service 🕵️‍♂️" or "Anamoly Detector" - Analyzes CloudTrail logs, VPC flow logs, DNS logs
- "Inspector = Vulnerability Scanner 🔍" - EC2, ECR, Lambda
- "Macie = PII Detector 📦" - S3

---

## Must-Know Core Concepts

### 🕵️‍♂️ Amazon GuardDuty

- **Threat detection service** that uses machine learning and threat intel (from AWS + partners).
- Monitors:
  - AWS CloudTrail logs
  - VPC Flow Logs
  - DNS logs
- Detects:
  - Compromised instances
  - Unusual API activity
  - C2 traffic (e.g., communication with known bad IPs)
- **Regional service** with multi-account support (via delegated admin).

### 🔍 AWS Inspector

- **Automated vulnerability scanner** for:
  - EC2 instances
  - Lambda functions
  - Container images (ECR)
- Scans for:
  - OS vulnerabilities (CVEs)
  - Network accessibility issues
  - Software version mismatches
- Automatically rescans on instance state change or image push.
- Integrated with **EventBridge, SNS, Security Hub**.

### 📦 Amazon Macie

- **Data classification service** focused on S3 buckets.
- Uses machine learning to detect:
  - PII (names, credit cards, etc.)
  - Custom sensitive data types
- Automatically discovers **public S3 buckets** and alerts.
- Fully managed, supports multi-account setups.
- Privacy-focused environments (HIPAA, GDPR) benefit most.

---

## Nuances & Edge Cases

- GuardDuty does **not block threats**, only alerts — integrate with Security Hub / EventBridge for action.
- Inspector supports **agentless scanning** via Systems Manager or ECR.
- Macie **only supports S3** — does not work on EBS, RDS, or DynamoDB.
- Macie pricing is **based on scanned object size**, can be costly at scale.

---

## Exam Pointers

- 🧠 GuardDuty = Detects **suspicious behavior**, uses **logs**.
- 🔍 Inspector = Finds **vulnerabilities** in EC2, Lambda, ECR.
- 📦 Macie = Scans **S3 for sensitive data** like PII.
- ❗ None of these are enforcement tools — they detect and report.
- 💡 Use **Security Hub** to centralize findings from all three.

