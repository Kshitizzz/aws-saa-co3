# IGW vs NAT Gateway vs Egress-Only IGW

## Memory Hook

- “IGW = Two-way public”
- “NAT GW = Outbound-only for private”
- “EOIGW = NAT for IPv6”

---

## ✅ Core Concept: Stateful Behavior

- All three (IGW, NAT GW, EOIGW) are **stateful**:
  > If traffic is initiated **from inside the VPC**, **response traffic is allowed**.

---

## 📦 Internet Gateway (IGW)

- **Supports Egress** ✅: VPC → Internet
- **Supports Ingress** ✅: Internet → VPC (only if:
  - Resource has **public IP**
  - Route Table includes IGW
  - Security Group allows it)
- **Used for**: EC2 with public IPs, ALBs, Lambdas in public subnets

---

## 📤 NAT Gateway (IPv4 only)

- **Supports Egress** ✅: Private subnet EC2 → Internet
- **Ingress?** ❌ No inbound connections from the internet
- **Return traffic allowed**: Only if **initiated from inside**
- **Used for**: Outbound internet access from **private subnets**
- **Security behavior**: Prevents exposure — no unsolicited inbound traffic

---

## 🌐 Egress-Only Internet Gateway (EOIGW)

- **Supports Egress** ✅: IPv6 → Internet
- **Ingress?** ❌ Not allowed
- **IPv6 only**
- **Return traffic allowed**: Yes, stateful
- **Used for**: EC2s in private subnets with IPv6 that need outbound internet

---

## 📌 Summary Comparison Table

| Gateway Type         | Outbound (Egress) | Inbound (Ingress) | Stateful | Protocol Support |
|----------------------|-------------------|--------------------|----------|------------------|
| **IGW**              | ✅ Yes            | ✅ Yes             | ✅ Yes   | IPv4 + IPv6      |
| **NAT Gateway**      | ✅ Yes            | ❌ No              | ✅ Yes   | IPv4 only        |
| **EOIGW (IPv6 only)**| ✅ Yes            | ❌ No              | ✅ Yes   | IPv6 only        |

---

## 🧠 Exam Pointers

- “Can EC2 in public subnet be accessed from internet?” → ✅ Yes (via IGW + public IP)
- “Can EC2 in private subnet use NAT Gateway for inbound traffic?” → ❌ No
- “Need to allow outbound-only IPv6 traffic?” → ✅ Use EOIGW
- “Do any of these require SG/NACL rules?” → ✅ Yes — SG/NACL must still explicitly allow ports/protocols
