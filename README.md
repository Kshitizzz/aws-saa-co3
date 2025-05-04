my notes for aws saa co3 cert exam

here is the study plan I followed (thanks to ChatGPT): https://chatgpt.com/s/dr_681488a37c2c81919fb138a6f9f3578c


intermediate study plan as of 4th May Sunday:

# AWS SAA-C03 Study Plan (Intermediate Phase)

## Memory Hook

- "Edge first, then monitor, then network the beast."
- "Protect > Route > Watch > Wire"

---

## ✅ Phase 1: Identity & Security (Completed)

| Topic                            | Status   | Notes                                        |
|----------------------------------|----------|----------------------------------------------|
| IAM, Policies, Permission Boundaries | ✅ Done  | Identity foundation                          |
| AWS KMS + Encryption Models      | ✅ Done  | Envelope encryption, MRK, CSE/SSE clarity    |
| AWS Organizations + SCPs         | ✅ Done  | Org-wide controls, central policy management |
| AWS WAF, Shield, Firewall Manager | ✅ Done | Layer 7 protection + DDoS + central enforcement |
| GuardDuty, Macie, Inspector      | ✅ Done  | Threat detection, data classification, CVE scan |

---

## 🌐 Phase 2: Edge Services (Now)

| Topic                  | Status   | Notes                                                  |
|------------------------|----------|--------------------------------------------------------|
| AWS Certificate Manager (ACM) | ✅ Done  | TLS termination, cert automation, CloudFront & ALB    |
| **CloudFront**         | 🔜 Next  | Global CDN, cache, WAF integration, must-do before VPC |
| **AWS Global Accelerator** | 🔜 Next | TCP/UDP routing, latency optimization, Anycast IPs     |

---

## 📊 Phase 3: Monitoring & Audit Services

| Topic              | Status   | Notes                                                  |
|--------------------|----------|--------------------------------------------------------|
| AWS CloudTrail     | 🔒 Upcoming | Logs *who did what* — API activity tracker            |
| AWS CloudWatch     | 🔒 Upcoming | Logs, metrics, alarms for observability               |
| Amazon EventBridge | 🔒 Upcoming | Event routing and automation (WAF, GuardDuty triggers)|
| AWS Config         | 🔒 Upcoming | Resource drift detection, config history              |
| AWS Security Hub   | 🔒 Upcoming | Centralize security alerts (GuardDuty, Inspector)     |

---

## 🛠️ Phase 4: Core Networking & DNS

| Topic                 | Status   | Notes                                                |
|-----------------------|----------|------------------------------------------------------|
| VPC Basics            | 🔒 Upcoming | Subnets, routing, NAT/IGW, flow logs                |
| VPC Endpoints / Transit Gateway | 🔒 Upcoming | Advanced networking patterns                      |
| Route 53              | 🔒 Upcoming | DNS-level routing, latency/geolocation awareness    |

---

## ⚠️ Guidance

- ✅ **CloudFront & Global Accelerator should be done before VPC.**
- 🔁 **Monitoring tools** make more sense *after* learning how workloads are exposed via edge services.
- 🔒 Do **Route 53 after VPC**, when IP/subnet routing makes sense.
