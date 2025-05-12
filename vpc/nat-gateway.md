# NAT Gateway (Managed Option for Outbound Internet)

## Memory Hook

- “Private Subnet → NAT Gateway → Internet”
- “Gate out, but never gate in.”

---

## ✅ Must-Know Core Concepts

- NAT Gateway enables **resources in private subnets to access internet**
- **Managed by AWS** — no patching, scaling, or admin work
- Always deployed in a **public subnet**
- **One-way only**: allows **outbound access**, not inbound
- Must be associated with an **Elastic IP**

---

### 🔁 How It Works

1. Private subnet EC2 sends packet to `0.0.0.0/0`
2. Route table forwards to NAT Gateway in public subnet
3. NAT Gateway uses its **Elastic IP** to send traffic to internet
4. Response is routed back → to the EC2 (via source IP tracking)

---

## ⚙️ Required Setup

| Component          | Required Configuration                              |
|-------------------|------------------------------------------------------|
| Subnet             | NAT Gateway lives in **public subnet**              |
| Elastic IP         | Mandatory                                            |
| Route Table (Private Subnet) | Route `0.0.0.0/0 → nat-gw-id`                  |
| IGW in VPC         | Needed so NAT Gateway can reach internet            |

---

## 📌 Exam Pointers

- “Private EC2 needs internet access, but should remain unreachable from public internet” → ✅ Use NAT Gateway
- “AWS-managed, scalable solution for outbound traffic” → ✅ NAT Gateway
- “Can I SSH into EC2 behind NAT GW?” → ❌ No — it allows only **outbound**, not inbound

---

## ⚠️ Nuances & Gotchas

- **AZ-Scoped**: NAT Gateway is tied to one AZ — create **1 per AZ** for HA  
- NAT Gateway = regional service, but **placed in an AZ**
- You still need a **public subnet with route to IGW** to host the NAT Gateway
- **Costs**:
  - Hourly charge (e.g., ~$0.045/hr)
  - Data processing charge (~$0.045/GB)

---

## 🔁 NAT Gateway vs NAT Instance

| Feature               | NAT Gateway (Modern)      | NAT Instance (Legacy)      |
|------------------------|---------------------------|-----------------------------|
| Managed by AWS         | ✅ Yes                    | ❌ No                       |
| Scaling                | ✅ Automatic (up to 45Gbps)| ❌ Manual (EC2 size)        |
| AZ-aware               | ✅ One per AZ             | ❌ Must build HA manually   |
| Elastic IP required    | ✅ Yes                    | ✅ Yes                      |
| Cost                   | 💰 More expensive at idle | 💰 Cheaper at low scale     |
| Admin effort           | ✅ Minimal                | ❌ High (routing, patching) |

---

## 🧠 When to Use

- ✅ Always prefer over NAT Instance in **production, scalable setups**
- ✅ For serverless workloads or EC2s that need to **pull from the internet**
- ❌ Not usable for inbound SSH or public access
