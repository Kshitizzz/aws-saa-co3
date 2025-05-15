# AWS Direct Connect

## Memory Hook
- “Fiber to the Cloud”
- “No internet, just direct AWS backbone”

---

## ✅ Must-Know Core Concepts

- **DX** is a **private network connection** between your data center and AWS
- Connects through an **AWS Direct Connect location**
- Bandwidth options: **1 Gbps, 10 Gbps, 100 Gbps**
- Traffic **never touches the public internet**
- Common for:
  - Financial, healthcare, compliance-sensitive workloads
  - High throughput or low latency needs
  - VPN over internet not good enough

---

## 🛠️ DX Architecture Flow

- On-Premises Router ↕ (Physical Fiber Link)
- AWS DX Location (PoP)↕ (AWS Backbone)
- Virtual Interface (VIF)↕VPC (via VGW or TGW)


---

## 🔄 Virtual Interfaces (VIFs)

| VIF Type        | Purpose                                     |
|------------------|---------------------------------------------|
| **Private VIF**  | Connect to your **VPC** via VGW or TGW      |
| **Public VIF**   | Access **AWS public services** (S3, STS)    |
| **Transit VIF**  | Connect DX to **Transit Gateway**           |

🧠 You choose VIF type based on what you're connecting to.

---

## 🔁 DX vs VPN

| Feature            | VPN (Site-to-Site)            | Direct Connect (DX)                  |
|---------------------|-------------------------------|---------------------------------------|
| Medium              | Public Internet               | Dedicated fiber                      |
| Encryption          | ✅ Built-in (IPsec)           | ❌ Not encrypted (add MACsec if needed) |
| Latency             | ❌ Variable                   | ✅ Consistent and low                |
| Setup time          | ✅ Quick (hours)              | ❌ Slow (weeks to provision)         |
| Cost                | 💰 Moderate                   | 💰💰 High (but no data egress fees)   |
| Bandwidth           | Up to 1.25 Gbps               | 1–100 Gbps                           |

---

## ⚠️ Nuances & Gotchas

- You can **combine DX + VPN** for high-availability:
  - DX = Primary (low latency)
  - VPN = Backup (internet fallback)
- DX itself has **no encryption** — traffic is private but plaintext unless you add:
  - **MACsec (Layer 2)**
  - or **IPsec over Direct Connect**
- You pay per **port-hour + data transferred**

---

## 📌 Exam Pointers

- “Need secure, low-latency, high-throughput link?” → ✅ Direct Connect
- “Need redundant, encrypted failover?” → ✅ Direct Connect + VPN
- “Can I use DX to access S3?” → ✅ Yes, via **Public VIF**
- “Connect multiple VPCs to DX?” → ✅ Use **Transit Gateway + Transit VIF**
- “Does DX provide encryption?” → ❌ No — use extra layers

