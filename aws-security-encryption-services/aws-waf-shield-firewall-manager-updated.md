# AWS WAF, Shield, and Firewall Manager

## Memory Hook

"Web ACL stops bad requests, Shield stops large-scale attacks, Firewall Manager controls everything across accounts."

---

## Must-Know Core Concepts

| Service               | Purpose                                                    | Layer     | Regional/Global | Where it Applies                     |
|-----------------------|------------------------------------------------------------|-----------|------------------|--------------------------------------|
| AWS WAF (Web ACL)     | Blocks malicious HTTP requests (SQLi, XSS, bots, IPs)      | Layer 7   | Global + Regional | ALB, CloudFront, API Gateway, AppSync |
| AWS Shield Standard   | Auto DDoS protection (free, always-on)                     | Network   | Global           | All AWS endpoints                     |
| AWS Shield Advanced   | Paid tier – DDoS protection + 24/7 DRT + cost protection    | Network   | Global           | CloudFront, ALB, Route 53, Elastic IP |
| AWS Firewall Manager  | Central policy manager across org accounts (via AWS Org)   | Control   | Regional         | All of above + SG auditing            |

---

## Nuances & Edge Cases

- WAF uses **Web ACLs** (rules based on URI, headers, etc.) and supports **Managed Rule Groups** (e.g., AWSManagedRulesSQLiRuleSet).
- **Shield Advanced** includes **cost protection**, integration with WAF, and **custom mitigation** strategies.
- **Firewall Manager** requires **AWS Organizations** and **Org-wide SCPs** for central policy enforcement.
- WAF is regional for ALB, API Gateway and AppSync, **global only for CloudFront**.

---

## Web ACLs vs Security Groups vs NACLs

- **Web ACLs** (WAF): App layer, supports managed rules, can rate-limit or block based on content.
- **Security Groups**: Stateful, instance-level, cannot deny, only allow rules.
- **NACLs**: Stateless, subnet-level, supports both allow and deny.

---

## Exam Pointers

- Web ACL is **for HTTP/HTTPS L7 traffic filtering** – attaches to ALB, CF, API Gateway.
- Shield Standard is **free**, always-on — but Advanced gives you full **DDoS protection + support**.
- Firewall Manager only works **with AWS Organizations** and enables **centralized management** of WAF/Shield/Security Group policies.
- WAF is **regional** except for **CloudFront**.

