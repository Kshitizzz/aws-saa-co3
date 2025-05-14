# AWS Site-to-Site VPN

## Memory Hook
- “On-prem ↔ AWS = Encrypted tunnel over public internet”
- “CGW initiates, VGW terminates”

---

## ✅ Key Concepts

- **Site-to-Site VPN** creates a **secure IPsec VPN tunnel** over internet
- Used to connect **on-prem data center** to an **AWS VPC**
- Supports static or dynamic routing (BGP)
- **Dual tunnel setup** for HA (active-active or active-passive)

---

### 🔗 Components

| Component           | What It Represents                            |
|----------------------|------------------------------------------------|
| **Customer Gateway (CGW)** | On-prem device (firewall/router/VPN) — your side |
| **Virtual Private Gateway (VGW)** | AWS-side VPN termination point (attached to VPC) |

---

## 📡 Packet Flow

- On-Prem LAN —[Router]— CGW —[Encrypted Tunnel]— VGW —[Route Table]— VPC

- VGW must be **attached to the VPC**
- Subnet route table must include `OnPremCIDR → VGW`

---

## 💥 Gotcha #1: ICMP (Ping) Doesn’t Work?

- Even if VPN is up, you can’t ping EC2 unless:
  ✅ **Security Group allows ICMP inbound**
  ✅ NACLs allow it too

🧠 By default, **SGs block ping (ICMP)** — needs custom rule!

---

## 🔁 Gotcha #2: Transitive Routing Doesn’t Work

- **Site-to-Site VPN is NOT transitive by default**
- You cannot go: Site-A → AWS VPC → Site-B

without Transit Gateway

✅ If you want **hub-and-spoke VPN** topology → use **Transit Gateway** with multiple VPN attachments.

---

## 🤡 What is PPN (Physically Private Network)? 😄

- No such AWS term, but logically:
- A **Direct Connect (DX)** circuit is **a physical private network** between your DC and AWS
- So:  
🔹 **VPN** = Logical, encrypted tunnel over internet  
🔹 **DX** = Physically private fiber network (expensive, fast)

---

## 🧠 Gotcha #3: Route Table Setup Required

Even if VPN is up:
- VPC Route Table must route `OnPremCIDR → VGW`
- CGW device must route `VPC CIDR → Tunnel IP`

---

## 📌 Exam Pointers

- “Connect DC to AWS securely over internet?” → ✅ Site-to-Site VPN
- “Dual tunnel VPN connection?” → ✅ Redundancy (2 IPsec tunnels per VPN)
- “Transitive traffic between 2 on-prem sites via VPC?” → ❌ Not supported without Transit Gateway
- “VPN up but ping fails?” → ✅ Check SG/NACL for ICMP
- “What’s the AWS endpoint in S2S VPN?” → ✅ Virtual Private Gateway (VGW)
- “Need to control VPN setup on your side?” → ✅ Configure Customer Gateway manually

---

## 🧠 Summary: VPN vs (Unofficial) PPN

| Feature           | Site-to-Site VPN (VPN)       | Direct Connect (“PPN”)               |
|-------------------|-------------------------------|--------------------------------------|
| Medium            | Public internet               | Private leased line                  |
| Speed             | Up to 1.25 Gbps               | 1–100 Gbps                           |
| Encryption        | ✅ Encrypted (IPSec)           | ❌ Must add MACsec for encryption     |
| Cost              | 💰 Pay per connection/hour     | 💰💰💰 High fixed circuit cost         |
| Setup Time        | Quick                         | Weeks/months                         |
| Transitive Support| ❌ Without TGW                 | ✅ With TGW                           |


