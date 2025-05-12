# NAT Instance (Legacy Option)

## Memory Hook

- “Private EC2 → NAT → Internet”
- “Acts like a one-way door to the internet for private resources”

---

## ✅ Must-Know Core Concepts

- A **NAT Instance** is just an EC2 instance configured as a **router + IP forwarder**
- Used to allow **private subnet EC2s to access internet**
- Must be placed in a **public subnet**
- Must have:
  - **Public IP**
  - **Route table entries** from private subnet pointing to NAT instance

---

## ⚙️ Required Setup

| Component         | Requirement                                         |
|------------------|-----------------------------------------------------|
| Subnet            | NAT in public subnet                                |
| EC2 Config        | Disable Source/Destination Check                    |
| Route Table       | Private subnet routes `0.0.0.0/0` → NAT instance    |
| SG/NACL           | Allow inbound from private subnet, outbound to internet |

---

## 📌 Exam Pointers

- “Private EC2s need internet but must stay private?” → ✅ Use NAT (Instance or Gateway)
- “Want to customize traffic handling or use your own AMI?” → ✅ Use NAT Instance
- “AWS-managed, auto-scaling?” → ❌ Not supported by NAT instance → use **NAT Gateway**

---

## ⚠️ Nuances & Limitations

- **High availability?** You must manually create and manage failover instances in each AZ
- **Scaling?** Manual — use bigger EC2 types or custom AMIs
- **Security?** You manage the EC2 security group and patching
- **Cost?** Can be cheaper than NAT Gateway at very low scale, but more effort to maintain

---

## 🔁 NAT Instance vs NAT Gateway (Comparison)

| Feature               | **NAT Instance**           | **NAT Gateway**              |
|------------------------|----------------------------|-------------------------------|
| Managed by AWS         | ❌ No                       | ✅ Yes                        |
| High Availability      | ❌ Manual                   | ✅ Auto (multi-AZ aware)      |
| Performance            | ⚠️ Depends on EC2 size     | ✅ Scales to 45 Gbps          |
| Elastic IP required    | ✅ Yes                      | ✅ Yes                        |
| Cost                   | 💰 Cheaper for <~1GB/day   | 💰 Higher fixed hourly + data cost |
| Setup Effort           | ⚠️ High (custom routing)   | ✅ Minimal                    |

---

## 🧠 When to Use

- ✅ Low-traffic, cost-sensitive workloads
- ✅ Custom routing/firewall logic (e.g., proxy, packet inspection)
- ❌ Not for production-scale, multi-AZ architectures (use NAT Gateway)

