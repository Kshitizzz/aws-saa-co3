
# AWS WAF vs Shield vs Network Firewall vs Firewall Manager

## Memory Hook

- “WAF for apps, Firewall for VPCs, Shield for DDoS, Manager to rule them all”

---

## ✅ 1. AWS WAF (Web Application Firewall)

- Works at **Layer 7 (HTTP/HTTPS)**
- Filters **web traffic** by:
  - IP
  - Geo location
  - User-Agent
  - Query strings
  - SQL injection / XSS

### 📌 Used with:
- ✅ CloudFront
- ✅ Application Load Balancer
- ✅ API Gateway
- ✅ AWS AppSync

---

## ✅ 2. AWS Shield

### 🚨 Shield Standard:
- Free for all AWS customers
- Automatic DDoS protection (L3/L4)
- Protects:
  - ✅ Route 53
  - ✅ CloudFront
  - ✅ ALB/NLB
  - ✅ Global Accelerator

### 🛡️ Shield Advanced (Paid):
- Includes:
  - Real-time attack detection
  - 24/7 DDoS response team (DRT)
  - Up to $300K AWS bill protection
  - Visibility via CloudWatch and AWS Firewall Manager

---

## ✅ 3. AWS Network Firewall

- **Operates at VPC boundary** (Layer 3/4/7)
- Stateful and stateless packet-level rules
- Supports:
  - IP/port/protocol filtering
  - DNS domain filtering
  - TLS SNI filtering
- Route traffic via:
  - **Gateway Load Balancer**
  - **Transit Gateway**

---

## ✅ 4. AWS Firewall Manager

- **Centralized policy enforcement service**
- Manages:
  - AWS WAF rules
  - AWS Shield Advanced protections
  - AWS Network Firewall deployments
- ✅ Used in **multi-account AWS Organizations**
- ✅ Auto-applies policies to new resources/accounts

---

## 📌 Layer-by-Layer Summary

| Service               | Layer        | Scope                   | Use Case                                      |
|------------------------|--------------|--------------------------|-----------------------------------------------|
| **AWS WAF**           | L7 (App)     | Web-facing services      | Block XSS, SQLi, bad IPs on ALB/API Gateway   |
| **AWS Shield**        | L3/L4        | Edge (DDoS protection)   | Stop SYN floods, UDP reflection, L3 DoS       |
| **Network Firewall**  | L3–L7        | VPC boundary             | Filter internal VPC traffic, enforce IP/FQDN  |
| **Firewall Manager**  | Control Plane| Multi-account, global    | Consistent policy management across org       |

---

## 🧠 Exam Pointers

- “How to block SQL injection on API Gateway?” → ✅ AWS WAF
- “Need L7 firewall on ALB?” → ✅ AWS WAF
- “How to mitigate volumetric DDoS attacks?” → ✅ AWS Shield
- “Want DNS-level filtering for EC2 traffic?” → ✅ AWS Network Firewall
- “Need centralized WAF policy for all accounts?” → ✅ AWS Firewall Manager

