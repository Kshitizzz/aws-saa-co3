# Amazon VPC – CIDR Blocks

## Memory Hook

- “CIDR = IP ka ZIP code”
- “It defines the size of your network and how you split it up”

---

## ✅ Must-Know Core Concepts

- CIDR = **Classless Inter-Domain Routing**
- Format: `X.X.X.X/XX` (e.g., `10.0.0.0/16`)
- `/16` means 2⁰⁶ = 65,536 IPs
- Minimum = `/28` → 16 IPs  
  Maximum = `/16` → 65,536 IPs (VPC limit)

### AWS Reserved IPs (per subnet)
- 5 IPs are always reserved:
  - `.0` Network address
  - `.1` VPC router
  - `.2` DNS
  - `.3` Reserved
  - `.255` Broadcast address

🧠 *So if you create a `/24` subnet (256 IPs), you'll only get 251 usable IPs.*

---

## 🧪 Example CIDRs

| CIDR Block     | Usable IPs | Description                      |
|----------------|------------|----------------------------------|
| `10.0.0.0/16`  | 65,531     | Large VPC                        |
| `10.0.1.0/24`  | 251        | Single subnet (small team/app)   |
| `10.0.1.128/25`| 123        | Half a /24, used in subnetting   |

---

## 📌 Exam Pointers

- “How many IPs are in `/26`?” → ✅ 64 – 5 = 59 usable
- “Which block allows most hosts?” → ✅ `/16` (within VPC limits)
- “What size subnet supports exactly 6 EC2s?” → ✅ `/29` (8 – 5 = 3 → too small), so use `/28`
- “Can I change VPC CIDR after creation?” → ✅ Yes (you can add secondary CIDR blocks now)

---

## 🔄 CIDR Strategy in VPC Design

| Goal                     | Recommendation                     |
|--------------------------|-------------------------------------|
| Max flexibility          | Start with `/16` for VPC            |
| Subnet sizing            | Use `/24` for app subnets, `/28` for NAT, `/26` for AZ-specific services |
| Multi-region compatibility | Avoid overlapping CIDRs           |
| Isolation or tiering     | Separate subnets with distinct blocks (e.g., `/24`, `/25`) |

