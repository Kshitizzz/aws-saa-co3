# AWS Network Firewall

## Memory Hook

- “SGs for EC2s, but Firewall for VPC perimeters”
- “Zero Trust = Central Control”

---

## ✅ Must-Know Core Concepts

- **Fully-managed firewall** service at **VPC level**
- Works via **Gateway Load Balancer Endpoint** or subnet-level routing
- Supports **stateful and stateless rules**
- Operates at:
  - Layer 3 (IP)
  - Layer 4 (TCP/UDP ports)
  - Layer 7 (FQDN, HTTP method, TLS SNI, etc.)

---

## 🧠 Fine-Grained Controls

| Control Type         | Example                                                       |
|----------------------|---------------------------------------------------------------|
| **Stateless**        | Drop traffic from specific CIDRs or protocols                 |
| **Stateful**         | Allow only TCP 443 to `*.example.com` with alerting           |
| **FQDN filtering**   | Block access to `facebook.com` or allow `api.mydomain.com`    |
| **Deep Packet Rules**| Deny HTTP POST but allow GET, or scan TLS SNI headers         |

---

## 🧱 Architecture Setup

- Deployed as a **firewall endpoint in a dedicated subnet**
- Route traffic through that subnet using **VPC Route Tables**
- Integrates with **Transit Gateway** for centralized multi-VPC firewalling
- Traffic routing via **Gateway Load Balancer** or **explicit routing**

---

## 📦 Rule Groups

| Rule Type     | Functionality                                  |
|---------------|------------------------------------------------|
| **Stateless** | First line filter — IPs, ports, protocols      |
| **Stateful**  | Tracks sessions — can inspect headers & payload|

- Managed rule groups also available (e.g., AWS Threat Intel Feeds)

---

## 📌 Exam Pointers

- “Want to block access to malicious domains?” → ✅ Use AWS Network Firewall with DNS/FQDN filters
- “How to centrally enforce firewall policies across VPCs?” → ✅ TGW + AWS Network Firewall
- “Do Security Groups provide same control?” → ❌ No — SGs are only Layer 4 & per-ENI
- “Want to allow only HTTPS, no other traffic from VPC?” → ✅ Define stateful allow-only rules

---

## ⚠️ Gotchas

- Traffic must be **routed through firewall subnet**
- Not a replacement for WAF (WAF = App Layer 7 on ALB/CF)
- Cost is per endpoint + per GB of traffic analyzed
- Stateful rules only apply **after stateless pass**

