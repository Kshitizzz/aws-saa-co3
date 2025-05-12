# Internet Gateway vs NAT Gateway

## Memory Hook
- “IGW = Come and Go”
- “NAT Gateway = Go Only”

---

## ✅ Purpose Comparison

| Feature                | **Internet Gateway (IGW)**                | **NAT Gateway (NATGW)**                         |
|------------------------|-------------------------------------------|-------------------------------------------------|
| **Direction**           | Inbound + Outbound                        | Outbound only                                   |
| **Used by**             | Public subnets with public IPs            | Private subnets (no public IPs)                |
| **Public IP Needed**    | ✅ Yes (on EC2)                            | ❌ No (private EC2 stays private)              |
| **Managed by AWS**      | ✅ Yes                                     | ✅ Yes                                           |
| **Supports inbound SSH**| ✅ Yes (if SG allows)                     | ❌ No                                            |
| **Supports outbound curl/wget** | ✅ Yes                        | ✅ Yes                                           |
| **AZ-Aware?**           | ❌ No (VPC-level resource)                 | ✅ Yes (must deploy one per AZ for HA)         |
| **Cost**                | 💸 Free                                    | 💸 Charged hourly + data processing            |

---

## 🧠 Exam Pointers

- “Want EC2 to host a web app?” → ✅ IGW + public subnet + public IP
- “Want private EC2 to fetch updates from internet?” → ✅ NATGW + route table
- “Does NATGW allow incoming connections?” → ❌ No (egress-only)
- “Can IGW be used by private subnets?” → ❌ No — unless public IP assigned + route exists

