# AWS Networking Costs per GB – Optimization Cheatsheet

## Memory Hook

- “Private IP = free”
- “Same AZ = cheapest”
- “Public = priciest”
- “Egress = always costs more than ingress”

---

## ✅ 1. Intra-VPC Traffic (First Diagram)

| Traffic Pattern                   | Cost         |
|----------------------------------|--------------|
| Same AZ, private IP              | ✅ Free       |
| Different AZs, private IP        | 💲 $0.01/GB   |
| Using Public/Elastic IP (anywhere)| 💲 $0.02/GB   |
| Ingress to EC2 (any)             | ✅ Free       |

🧠 Use **private IPs + same AZ** whenever possible  
❗Public IP communication between two EC2s = most expensive intra-region

---

## ✅ 2. Egress Minimization (Second Diagram)

| Direction            | Cost Profile           | Optimization Tip                                      |
|----------------------|------------------------|--------------------------------------------------------|
| AWS → On-Prem (egress)| 💲 Expensive            | ❌ Avoid heavy data pulling from AWS to corp DC        |
| On-Prem → AWS (ingress)| ✅ Free               | ✅ Do data fetching inside AWS and return only results |

🧠 Shift logic **closer to data** (inside AWS) to minimize egress  
🏷️ **Direct Connect** (co-located) further reduces egress cost

---

## ✅ 3. S3 Data Transfer Pricing (Third Diagram)

| Path                                | Cost        |
|-------------------------------------|-------------|
| S3 → Internet                       | 💲 $0.09/GB  |
| S3 + Transfer Acceleration → Internet | 💲 $0.13–$0.17/GB |
| S3 → CloudFront                     | ✅ $0.00/GB  |
| CloudFront → Internet               | 💲 $0.085/GB |
| S3 → S3 Cross-Region Replication    | 💲 $0.02/GB  |

🧠 Optimization:
- ✅ Use **CloudFront** for public content (cheaper than S3 direct)
- ❌ Avoid S3-to-internet direct unless needed
- ✅ Use **same-region replication** wherever possible

---

## ✅ 4. NAT Gateway vs VPC Endpoint (Fourth Diagram)

| Traffic to S3                      | Via NAT Gateway | Via VPC Endpoint |
|------------------------------------|------------------|------------------|
| Hourly Infra Cost                  | 💲 $0.045/hr     | ❌ None           |
| Data Processing / GB               | 💲 $0.045/GB     | ❌ None           |
| Cross-region S3 egress             | 💲 $0.09/GB      | 💲 $0.09/GB       |
| Same-region S3 egress              | ✅ $0.00         | ✅ $0.00          |

🧠 Key Strategy:
- ✅ Use **VPC Gateway Endpoints** (for S3/DynamoDB) to eliminate NAT charges
- ❌ Don’t send S3 traffic over NAT unless absolutely required

---

## 📌 General Cost-Optimization Principles

1. Prefer **Private IPs** → avoid public IP charges
2. Stay within the **same AZ** → no $0.01/GB AZ data charge
3. Use **VPC Endpoints** → eliminate NAT Gateway hourly + per-GB fees
4. **Push compute closer to storage** (especially with S3)
5. Minimize **egress** — it’s always more expensive than ingress
6. For heavy or predictable hybrid loads → use **Direct Connect**

