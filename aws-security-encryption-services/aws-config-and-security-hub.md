# AWS Security Hub & AWS Config

## Memory Hook

- "Security Hub = Your Security Control Room 🕹️"
- "Config = Your Detective with a Notebook 📓"

---

## 🛡️ AWS Security Hub

### Must-Know Core Concepts

- Central service to **aggregate and normalize findings** from:
  - GuardDuty
  - Inspector
  - Macie
  - IAM Access Analyzer
  - Firewall Manager
- Runs **automated security checks** using AWS best practices (CIS Benchmarks).
- Produces a **security score** for your account/organization.
- Integrates with EventBridge for automatic remediation.
- Multi-account support via **Delegated Admin**.

### Nuances & Edge Cases

- Only aggregates findings — does **not auto-remediate**.
- Supports integration with **custom or third-party tools** (e.g. Splunk, PagerDuty).
- Findings use **AWS Security Finding Format (ASFF)**.
- Paid per finding ingested, not per resource.

### Exam Pointers

- If the question says “aggregate security alerts from multiple AWS services” → **Security Hub**.
- If it asks for a **centralized security dashboard** across org → **Security Hub**.
- If a **CIS benchmark scan** or **security score** is mentioned → this is the one.

---

## 🔍 AWS Config

### Must-Know Core Concepts

- Tracks **configuration changes** across AWS resources.
- Stores config **history**, **timeline**, and **snapshots**.
- Can define **Config Rules** to assess compliance:
  - AWS-managed (e.g., “S3 buckets must be encrypted”)
  - Custom rules via Lambda
- Supports **remediation actions** via SSM Automation Docs.
- Multi-account, multi-region aggregator support.

### Nuances & Edge Cases

- **Regional** service, must be explicitly enabled per region.
- Stores data in **S3**; incurs cost based on resources tracked + evaluations.
- Does **not monitor usage**, only **configuration**.
- Integrates with:
  - CloudTrail (to identify who made the change)
  - Security Hub (to report non-compliance)

### Exam Pointers

- If you see “track config changes”, “detect drift”, or “audit compliance” → go with **AWS Config**.
- If you see “S3 bucket turned public” → **AWS Config** + **Rule Violation**.
- If question mentions “remediate non-compliance automatically” → AWS Config + SSM Automation.

