# AWS Global Accelerator

## Memory Hook
- “CloudFront caches, GA connects.”
- “GA = Global IP + Smart TCP traffic router”

---

## ✅ Must-Know Core Concepts

- **Global traffic accelerator** for **TCP and UDP** traffic.
- Improves **availability, performance, and failover** for global apps.
- Assigns 2 **static Anycast IPs** → routed via **AWS global edge network**.
- Routes traffic to the **nearest healthy regional endpoint**:
  - ALBs
  - NLBs
  - EC2 instances
  - Elastic IPs
- Uses **health checks** to detect failures and **redirect** to healthy regions.
- Supports **client affinity** (IP stickiness).
- Regional failover in **<30 seconds**.
- Managed service — no extra setup for BGP, DNS propagation, or IP whitelisting.

---

## 🌐 Anycast IPs vs Unicast IPs

| Concept     | Description                                                |
|-------------|------------------------------------------------------------|
| **Anycast** | One IP → advertised from multiple edge locations           |
|             | Client connects to *nearest* AWS edge via BGP routing      |
| **Unicast** | One IP → One specific server or location                   |
|             | No global distribution; routing is rigid                   |

🧠 **GA uses Anycast IPs**, so the same IP is reachable globally with **lowest latency path**.

---

## 🔁 Global Accelerator vs CloudFront

| Feature                | **Global Accelerator**                        | **CloudFront**                                |
|------------------------|-----------------------------------------------|------------------------------------------------|
| Protocols              | TCP, UDP                                      | HTTP, HTTPS only                               |
| Use Case               | Dynamic content, gaming, VoIP, real-time APIs | Static + dynamic web/app content               |
| Caching                | ❌ No caching                                  | ✅ Edge caching                                |
| Routing Logic          | IP-based (Anycast)                            | URL/path-based                                 |
| TLS Termination        | At endpoint (ALB/NLB)                         | At edge (TLS offload)                          |
| IP Type                | ✅ Static, Global IPs                          | ❌ DNS-based, changing IPs                     |
| Failover               | < 30 sec regional failover                    | Depends on origin + TTL                        |

---

## ⚠️ Nuances & Edge Cases

- You get **2 Anycast static IPs** — these are **global**, stable, and can be whitelisted by clients/firewalls.
- GA is great for **gaming, live video, SaaS, or real-time APIs**.
- No native support for caching or HTTP behavior — that’s for **CloudFront**.
- You can **pair CloudFront + GA** in complex workloads (e.g., CloudFront for static, GA for dynamic).

---

## 📌 Exam Pointers

- “Accelerate TCP/UDP traffic to multi-region endpoints” → ✅ Global Accelerator
- “Require static IPs for clients/firewalls” → ✅ GA
- “Regional failover in <1 min” → ✅ GA
- “Accelerate content delivery” → CloudFront (if static), GA (if TCP)
- “Need caching or Lambda@Edge” → ❌ Not GA, ✅ CloudFront
- “Your app has endpoints in multiple AWS Regions” → ✅ GA with failover

---

## 🔄 Global Accelerator & Failover

- Health checks run against endpoints.
- If primary region is unhealthy → client traffic is rerouted to **secondary region automatically**.
- All while keeping the **same static IPs** — no DNS TTL delay.
- Use **Route53 + health checks** if you want DNS-based failover (slower).
