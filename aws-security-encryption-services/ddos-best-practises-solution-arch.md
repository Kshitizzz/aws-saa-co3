# AWS Best Practices for DDoS Resilience

## Architecture - [aws-security-encryption-services/architectures/ddos-best-practises.png]

- courtesy of Stephane Maarek [udemy]

## Memory Hook

- "Shield at the edge, WAF at the door, Scale inside."
- "Edge = absorb & block, Core = scale & distribute"

---

## 🧱 Infrastructure Layer Defense

### BP1 – CloudFront

- Deliver content at edge.
- Caches static content closer to user → reduces origin load.
- Protects against SYN floods, UDP reflection, HTTP floods.
- Integrates with AWS WAF and Shield.

### BP1 – Global Accelerator

- Routes TCP/UDP traffic via AWS global network using Anycast IPs.
- DDoS protection via Shield Standard/Advanced.
- Use when backend is not compatible with CloudFront (e.g., non-HTTP).

### BP3 – Route 53

- Scalable DNS resolution with edge protection.
- Supports health checks, failover, geo-routing.
- Integrated with Shield Advanced for DNS-level attack protection.

### BP6 – Elastic Load Balancer (ALB/NLB)

- Distributes traffic across healthy targets in multiple AZs.
- Scales automatically during traffic spikes.
- Protects EC2 by abstracting backend IPs.
- Works with WAF (ALB) and Shield.

---

## 🔐 Application Layer Defense

### BP2 – AWS WAF (with CloudFront or ALB)

- Filter malicious requests at L7 (SQLi, XSS, IP block, rate-limits).
- Use **Managed Rule Groups** or custom rules.
- Protects API Gateway, AppSync, ALB, and CloudFront.
- Rate-based rules can block DDoS from abusive IPs automatically.

### BP4 – API Gateway

- Use in regional or edge-optimized mode.
- Protect endpoints with:
  - WAF rules (IP filtering, headers, request size)
  - API keys, usage plans, throttling
- Hides backend services (e.g., Lambda, EC2)

---

## 🚪 Attack Surface Reduction

### BP5 – Security Groups & NACLs
- **Security Groups**: Stateful, instance-level filtering.
- **NACLs**: Stateless, subnet-level filters with deny support.
- Use for IP whitelisting, port control at network level.
- Use **least privilege principle**: open only required ports.

### BP8 – AWS Transit Gateway + DX/VPN
- Connect VPCs and on-premises securely.
- Avoid direct internet exposure of workloads.
- Offload secure routing to AWS infra.

---

## ⚙️ Scaling & Resilience Mechanisms

### BP7 – EC2 with Auto Scaling Group
- Helps absorb burst traffic or flash crowd (e.g., marketing launch).
- Ensures backend stays responsive.
- Use lifecycle hooks to ensure warm-up before traffic hits.

---

## Exam Pointers

- 🧠 CloudFront + WAF = best L7 edge defense.
- 🔐 Shield Standard = Always on; Shield Advanced = Paid, with DRT support & cost protection.
- 🌐 Route 53 is DNS-level defense + geo-routing + health checks.
- ⚡ Global Accelerator = best for TCP/UDP, ALB/NLB endpoint acceleration + DDoS layer.
- 📈 Use Auto Scaling to defend against burst/floods at compute layer.
- 🔒 Use Security Groups/NACLs for internal IP/port filtering.
- 🔧 Use API Gateway + throttling + WAF to protect APIs from misuse.

