# NAT, NAT Gateway, VPC Endpoints & NACLs – Deepest Dive

## Memory Hook  
- “NAT = go out, not in”  
- “VPC Endpoint = AWS service in your private lane”  
- “NACL = subnet bouncer — stateless, first come first serve”

---

## ✅ What Is NAT?

> **NAT = Network Address Translation**  
Allows **private EC2s to access the internet**, **without being reachable from outside**

---

## ✅ NAT Gateway (NATGW)

| Property                 | Description                                                        |
|--------------------------|--------------------------------------------------------------------|
| **Managed by AWS?**      | ✅ Yes (scalable, HA in one AZ)                                   |
| **Public IP attached?**  | ✅ Yes (must be in public subnet)                                 |
| **Direction**            | ✅ Outbound only (private → public internet)                      |
| **Route required?**      | ✅ Route from private subnet to NATGW in public subnet            |
| **Support return traffic?** | ✅ Yes — stateful handling of responses                        |
| **Pricing**              | 💸 Charged per hour + per GB transferred                          |

---

## ✅ NAT Instance (Legacy Alternative)

| Property                 | Description                                            |
|--------------------------|--------------------------------------------------------|
| **DIY EC2?**             | ✅ Yes — self-managed                                  |
| **Scales?**              | ❌ No auto scaling — manual                            |
| **HA Setup?**            | ❌ You manage multiple AZs                             |
| **Traffic Logging?**     | ✅ Possible via iptables                               |

---

## ✅ NATGW vs IGW vs NLB (Comparison)

| Feature              | NATGW                | IGW                  | NLB (Public)             |
|----------------------|----------------------|-----------------------|--------------------------|
| Supports outbound?   | ✅ Yes (NAT)          | ✅ Yes (direct)       | ❌ Not designed for this |
| Supports inbound?    | ❌ No (return traffic only) | ✅ Yes (public IP) | ✅ With target groups     |
| Requires public subnet? | ✅ Yes            | ✅ Yes                | ✅ Yes                   |

🧠 **IGW + public IP → full two-way internet**  
🧠 **NATGW + route → outbound only from private subnet**

---

## ✅ VPC Endpoints – Secure AWS Service Access

> Private connections between your VPC and AWS services, **without public internet**

---

### 🔹 Interface Endpoints

> ENIs (Elastic Network Interfaces) provisioned in your subnet for private communication

| Feature               | Details                                        |
|------------------------|------------------------------------------------|
| AWS Services Supported | S3, Secrets Manager, API Gateway, KMS, etc.  |
| How?                   | Creates an ENI in your subnet                 |
| Protocol               | TCP (HTTPS)                                   |
| Can attach SGs?        | ✅ Yes — like any other ENI                   |
| Cost?                  | ✅ Per-hour + per-GB charges                  |

🧠 These show up in VPC as **ENIs**  
🧠 You access AWS service via a private DNS alias

---

### 🔹 Gateway Endpoints

> Specialized routing path to **S3 or DynamoDB**

| Feature           | Details                              |
|--------------------|--------------------------------------|
| AWS Services       | ✅ S3, DynamoDB only                |
| Setup              | Adds target in route table           |
| Uses Internet?     | ❌ No                                |
| SGs/NACLs apply?   | ✅ Yes                              |
| Cost?              | ✅ Free                             |

🧠 You don’t talk to ENIs here — just a route entry to "vpce-svc-XXXX"

---

## ✅ NACLs (Network Access Control Lists)

> Stateless firewall applied at **subnet level**  
Every subnet must be associated with a NACL (default if none custom)

---

### 🔍 Key Properties

| Feature               | Description                                |
|------------------------|--------------------------------------------|
| **Stateless?**         | ✅ Yes — both inbound and outbound must be allowed |
| **Order matters?**     | ✅ Yes — rule #100 beats rule #110         |
| **Allow/Deny?**        | ✅ Both supported                          |
| **Default behavior?**  | ✅ Default NACL allows all                 |
| **Custom behavior?**   | Default deny unless rule says allow        |

---

### ✅ When to Use NACLs

- Extra layer beyond SGs
- Restrict traffic to/from **entire subnet**
- Block specific **IP ranges** or ports globally

🧠 Unlike Security Groups:
- SGs = **stateful, ENI-level**
- NACLs = **stateless, subnet-level**

---

## ✅ Real-World Network Flow Example

1. EC2 in **private subnet** wants to pull OS patch from internet
2. It sends the request → NATGW → IGW → internet
3. Return traffic comes in, NATGW matches to state → response flows back
4. NACLs on subnet + SGs on ENI both must allow traffic

---

## 📌 Exam Pointers

- “How to allow EC2 in private subnet to connect to the internet?” → ✅ NAT Gateway + Route
- “Want EC2 to access S3 without public IP or NAT?” → ✅ S3 Gateway Endpoint
- “Need to secure VPC-to-AWS services with private link?” → ✅ Interface VPC Endpoint
- “Need stateless subnet-level block rule for IP range?” → ✅ Use NACLs
- “Need ENI that resolves to AWS service?” → ✅ Interface VPC Endpoint
- “Want public EC2 to serve internet traffic?” → ✅ Use IGW + public subnet + EIP or public IP
