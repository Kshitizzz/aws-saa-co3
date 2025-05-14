# VPC Peering

## Memory Hook

- “VPC Peering = One-to-One Private Tunnel”
- “No transitive routing allowed!”

---

## ✅ Must-Know Core Concepts

- **VPC Peering** connects **two VPCs privately** using AWS’s backbone
- Works across:
  - ✅ Same account
  - ✅ Different accounts
  - ✅ Same region or different regions
- Resources in both VPCs can communicate **using private IPs**

---

## 📦 Key Requirements

- VPCs must **not have overlapping CIDR blocks**
- **Both sides must update their route tables**
  - VPC-A must route `VPC-B CIDR → peering connection`
  - VPC-B must route `VPC-A CIDR → peering connection`
- **Security Groups** must allow traffic

---

## 🔁 Transitive Routing Not Allowed

> *If A peered to B, and B peered to C — A cannot talk to C.*

❌ No "hub and spoke" or chaining of peering  
✅ Use **Transit Gateway** for that use case

---

## ⚠️ Nuances & Gotchas

- You **can’t reference peered VPC’s DNS name** unless DNS resolution is explicitly enabled
- Must configure **both ends (route tables + SGs)** for it to work
- Peering does **not support IPv6 DNS by default**
- You can’t attach an **Internet Gateway** from one VPC to another via peering

---

## 📌 Exam Pointers

- “Two VPCs need to communicate privately without public IPs?” → ✅ VPC Peering
- “Need many-to-one VPC connectivity?” → ❌ Not Peering → ✅ Transit Gateway
- “VPCs have overlapping CIDRs?” → ❌ Peering not allowed
- “Traffic isn’t flowing?” → ✅ Check both route tables + SGs
- “A → B → C communication?” → ❌ Peering is **not transitive**

---

## 🤝 Common Peering Use Cases

| Scenario                              | VPC Peering Viable? |
|---------------------------------------|----------------------|
| Same-account VPC to VPC               | ✅ Yes               |
| Cross-account VPCs in same region     | ✅ Yes               |
| Cross-region VPCs (e.g. us-east-1 ↔ eu-west-1) | ✅ Yes (inter-region peering) |
| One VPC to multiple VPCs              | ❌ Prefer Transit Gateway |
