# 🧭 Route 53 – DNS Routing Mechanics

## Memory Hook
- "Route 53 is AWS’s phonebook and GPS — it finds **where** to go and **how** to get there."

---

## ✅ DNS Routing Policies in Route 53

| Policy Type         | When to Use                                                                 | Key Behaviors                                                                 |
|---------------------|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **Simple**          | One record, one destination                                                 | Random response if multiple records exist. No health checks.                  |
| **Weighted**        | Distribute % of traffic to multiple endpoints                              | Set weight for each record (e.g., 70/30). Supports health checks.             |
| **Latency-based**   | Route to the region with the lowest latency                                 | AWS latency is measured from user to resource. Health checks supported.       |
| **Failover**        | Route traffic to healthy resources only                                     | Primary and secondary endpoints. Uses health checks.                          |
| **Geolocation**     | Based on user’s location (continent/country/state)                          | Strict geo match. Good for compliance/regional content.                       |
| **Geo-proximity**   | Based on bias-adjusted distance from resource                               | Use with Route 53 Traffic Flow. Allows fine-grained tuning with **bias**.     |
| **Multivalue Answer** | Return multiple healthy IPs (up to 8), simulates round-robin             | Supports health checks. Great for basic load balancing.                       |

---

## ✅ Route 53 DNS Records Recap

| Record Type | Description                             | Example                                |
|-------------|-----------------------------------------|----------------------------------------|
| `A`         | IPv4 address                            | `app.example.com → 192.0.2.1`          |
| `AAAA`      | IPv6 address                            | `app.example.com → ::1`                |
| `CNAME`     | Alias to another domain                 | `www.example.com → app.example.com`    |
| `Alias`     | AWS-specific, points to AWS resource    | `example.com → ELB / S3 / CF`          |
| `MX`        | Mail servers                            | `10 mail.example.com`                  |
| `TXT`       | Verification/SPF/DKIM/DMARC             | `"v=spf1 include:..."`                 |

---

## ✅ Health Checks in Route 53

- You can attach health checks to:
  - EC2 instances, ELBs, custom IPs
  - CloudWatch alarms (e.g., CPU > 80%)
- Used in:
  - **Failover**, **Latency**, **Multivalue**, and **Weighted** routing.

---

## ✅ Alias vs CNAME (🔥 Exam Favorite)

| Feature        | `Alias` Record                            | `CNAME` Record                      |
|----------------|--------------------------------------------|-------------------------------------|
| AWS Resource? | ✅ Yes – ELB, CloudFront, S3, etc.         | ❌ No                               |
| Root Domain?  | ✅ Yes (`example.com`)                     | ❌ No – only subdomains (`www.`)    |
| Cost?         | ✅ Free (internal resolution)              | ❌ Billed as DNS queries             |

---

## Exam Pointers

- **CNAME** can’t be used on root domain, **Alias** can.
- Use **Latency policy** for region-aware performance.
- Use **Failover policy** for DR setups.
- Health checks are **optional**, but **required** in **Failover**.
- **GeoProximity** ≠ **Geolocation** → one uses bias/distance, one uses hard-coded location.

---

Let me know when you’re ready to cover **Traffic Flow**, **Private Hosted Zones**, or dive into **Resolver Inbound/Outbound** magic 🌐.
