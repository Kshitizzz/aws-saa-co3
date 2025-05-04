# AWS WAF vs Shield vs Firewall Manager

## Memory Hook

- "WAF = Rules walla bouncer, Shield = Bodyguard against DDoS, Firewall Manager = Security Manager of the club."
- Or
- "WAF filters, Shield protects, Firewall Manager enforces."

## Must-Know Core Concepts

### 🔰 AWS WAF (Web Application Firewall)

- Protects against common **Layer 7 web attacks** (SQLi, XSS, bot attacks).
- Allows setting **custom rules** or using **managed rule sets**.
- Integrated with:
  - Application Load Balancer (ALB)
  - API Gateway (REST and HTTP APIs)
  - AWS AppSync
  - AWS CloudFront (Global)
- Uses **Web ACLs** to define rules like allow, block, count.

### 🛡️ AWS Shield

- Provides **Layer 3 & 4 DDoS protection**.
- Two tiers:
  - **Shield Standard** (free, default)
  - **Shield Advanced** (paid, includes DRT support, cost protection, metrics)
- Protects ALB, NLB, CloudFront, Global Accelerator, Route 53.

### 🧠 AWS Firewall Manager

- **Centralized security policy enforcement** tool.
- Works across multiple AWS accounts via **Organizations**.
- Supports:
  - WAF rules
  - Shield Advanced protections
  - VPC security group policies
- Automatically applies rules to new resources in accounts.

## Nuances & Edge Cases

- WAF works only with **HTTP/HTTPS-based services** (no support for NLB/GA).
- Shield Advanced customers can get **attack cost protection** and help from AWS DRT.
- Firewall Manager requires:
  - **AWS Organizations**
  - **Management Account**
  - **Shield Advanced subscription**

## Exam Pointers

- 🧱 **Use AWS WAF** to block IPs, limit request rates, stop SQLi/XSS attacks.
- 🛡️ **Use AWS Shield Advanced** for high-risk apps needing DDoS protection + 24/7 support.
- 🧠 **Use Firewall Manager** in multi-account setups to enforce rules at org-level.
- ❌ WAF doesn’t support **NLB or Global Accelerator** (they're not HTTP-based).
- 🔁 WAF rules are reusable across regions and services via Web ACLs.
- 💸 Shield Advanced includes **cost protection** from scaling charges due to attacks.

## Regionality

- WAF → Regional, except when used with CloudFront, then it's global (because CloudFront is global).

- Shield Standard → Automatically global — applies to supported services regardless of region.

- Shield Advanced → Regional, but can protect global services (e.g., CloudFront, Route53).

- Firewall Manager → Global control across regions/accounts, but policy scope can be regionalized.
