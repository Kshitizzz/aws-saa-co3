# IGW vs NAT Gateway vs Egress-Only IGW

## Memory Hook

- Want IPV6 enables instances in private subnet to send requests out to resources on public internet
- use Egress only OGW
---

## ✅ Core Concept: Stateful Behavior

- Stateful, responses are allowed from public internet
- but, new connections requests are not allwed from the public internet, since Egress only
- ONLY one per VPC
- and, needs explicit routes in route tables
- remember, only for IPV6 enabled resources such as EC2s present in a PRIVATE subnet need this 
- hust like NATGW (which is for IPV4 instances in Private subnet)



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
