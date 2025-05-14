# AWS Transit Gateway (TGW)

## Memory Hook
- “One Hub to Route Them All”
- “Peering is personal, TGW is professional”

---

## ✅ Must-Know Core Concepts

- **Transit Gateway (TGW)** = AWS-managed network hub to connect:
  - VPCs
  - VPNs
  - Direct Connect
  - Eventually peered TGWs (inter-region)
- TGW simplifies large-scale network topologies using **hub-and-spoke**
- Each VPC connects to TGW using **Transit Gateway Attachment**

---

## 🧠 Routing Logic

- TGW has its own **route table(s)**
- Each **attachment (VPC or VPN)** can be associated with one or more TGW route tables
- You control which attachments can talk to each other by **managing TGW route tables**

---

## 🛠️ Common Use Cases

- Centralized shared services (DNS, logging, etc.)
- Multi-account VPC connectivity
- Connect on-prem VPN to many VPCs
- Simplify many-to-many VPC communication

---

## ⚠️ Nuances & Limits

- TGW is a **Regional resource**
  - For cross-region, use **Transit Gateway Peering**
- Bandwidth: **50 Gbps per attachment**
- Max 5,000 attachments per TGW (soft limit)
- TGW route tables ≠ VPC route tables — they are separate

---

## 📌 Exam Pointers

- “Need to connect 4 VPCs and 2 VPNs in a scalable way?” → ✅ Transit Gateway
- “Too many peering connections becoming unmanageable?” → ✅ Transit Gateway
- “Two VPCs in same region need to talk privately?” → ✅ VPC Peering (if simple)
- “Need transitive routing between VPCs?” → ✅ Only TGW supports it

---

## 🔄 Comparison: VPC Peering vs Transit Gateway

| Feature                    | **VPC Peering**             | **Transit Gateway**              |
|----------------------------|------------------------------|-----------------------------------|
| Type                       | Point-to-point               | Hub-and-spoke                     |
| Transitive routing         | ❌ Not supported              | ✅ Supported                      |
| Max scale                  | ~125 peering connections     | ✅ Thousands of attachments       |
| Routing complexity         | 🔺 High (manual per VPC)     | ✅ Centralized (via TGW route tables) |
| Cross-region support       | ✅ Yes                        | ✅ With TGW peering               |
| Cost                       | 💰 No data processing cost    | 💰 Charged per GB & per attachment hour |
| DNS support                | ❌ Must enable manually       | ✅ Built-in                       |
| Use case                   | Few VPCs, simple setup       | Large-scale, multi-account setup |

---

Let me know if you want a **diagram of VPC Peering vs TGW** or a **quiz to lock it in.**  
We’re deep into **networking mastery mode** now 🔥
