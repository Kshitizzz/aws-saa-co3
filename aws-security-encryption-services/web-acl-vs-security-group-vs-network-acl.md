# Web ACL vs Security Group vs Network ACL

## Memory Hook

"SG guards the door to your EC2, NACL guards the gate of your subnet, and Web ACL guards your application URL."

---

## Must-Know Core Concepts

| Feature                  | Web ACL (WAF)                | Security Group                | Network ACL (NACL)           |
|--------------------------|------------------------------|-------------------------------|------------------------------|
| OSI Layer                | Layer 7 (HTTP/S)             | Layer 3/4 (IP/TCP/UDP)        | Layer 3/4 (IP/TCP/UDP)       |
| Scope                    | ALB, CloudFront, API Gateway | ENI / EC2 / RDS instance      | VPC Subnet Level             |
| Stateful/Stateless       | Stateful                     | Stateful                      | Stateless                    |
| Inbound Rules            | Yes (URI, headers, etc.)     | Yes                           | Yes                          |
| Outbound Rules           | Yes                          | Yes                           | Yes                          |
| Protocol Awareness       | HTTP/S Only                  | IP/TCP/UDP                    | IP/TCP/UDP                   |
| Logging Supported        | Yes                          | Yes                           | Yes                          |
| Common Use               | Block attacks (SQLi, XSS)    | Allow secure ports (443/22)   | Basic subnet filtering       |
| Attach Target            | ALB, CF, API GW, AppSync     | EC2, ENI                      | Subnets                     |
| Rule Evaluation Order    | Priority-based (manual)      | All rules evaluated           | Numbered, lowest wins        |

---

## Nuances & Edge Cases

- Web ACL supports **managed rules**, rate limiting, and bot control.
- Security Groups do **not support deny rules**, only support allow rules.
- NACLs do support **explicit deny and allow**, but need manual egress rule config.
- Web ACL is **global for CloudFront**, **regional** for ALB/API Gateway.

---

## Exam Pointers

- Web ACL is **application layer protection** – think of OWASP threats.
- Security Groups = **stateful firewall** at instance level.
- NACL = **stateless subnet-level filter**, allows both ALLOW/DENY.
- **You can and should use all three together** for layered defense.

