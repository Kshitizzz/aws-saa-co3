# VPC Traffic Mirroring

## Memory Hook
- “WireShark for your VPC”
- “Watch traffic, don’t touch it”

---

## ✅ Must-Know Core Concepts

- **VPC Traffic Mirroring** lets you **copy network traffic** from **ENIs** in your VPC and **send it to monitoring appliances**
- Used for **packet-level monitoring**, not packet modification
- Supports **both ingress and egress traffic** from:
  - EC2 instances
  - Elastic Network Interfaces (ENIs)

---

## 🧠 Key Characteristics

| Property               | Description                                         |
|------------------------|-----------------------------------------------------|
| **Passive**            | ✅ Mirror only — doesn’t modify or interfere         |
| **Source**             | ENI (Elastic Network Interface)                     |
| **Target**             | ENI of monitoring appliance (e.g., EC2, GWLB)       |
| **Traffic Types**      | IPv4 and IPv6, TCP/UDP/ICMP                         |
| **Granular Control**   | Filter by packet header, port, protocol             |
| **Direction**          | Ingress, Egress, or both                            |
| **Limitation**         | No support for Nitro-based instances as targets     |

---

## ⚠️ Nuances & Gotchas

- Traffic mirror target must be in the **same AZ**
- Mirrored traffic is **raw packet data**, no application-level awareness
- You can create **multiple mirror sessions per source ENI**
- Requires **specific IAM permissions** (e.g., `ec2:CreateTrafficMirrorSession`)
- Not recommended for very high-throughput EC2s without filters — can overwhelm the target

---

## 🧪 Use Cases

- Intrusion detection and forensics (e.g., Suricata, Zeek)
- Performance monitoring
- Deep packet inspection
- Lawful intercept in regulated environments

---

## 📌 Exam Pointers

- “Need packet-level traffic analysis?” → ✅ Use VPC Traffic Mirroring
- “Want to route traffic to firewall for filtering?” → ❌ Not this → ✅ Use Gateway Load Balancer
- “Can traffic mirroring modify traffic?” → ❌ No, read-only
- “Can I mirror traffic between AZs?” → ❌ No, target must be in same AZ

---

## 🔁 VPC Traffic Mirroring vs Gateway Load Balancer

| Feature                | VPC Traffic Mirroring        | Gateway Load Balancer            |
|------------------------|------------------------------|-----------------------------------|
| **Mode**               | Passive                      | Inline                            |
| **Purpose**            | Observe & analyze            | Inspect & enforce                 |
| **Encapsulation**      | Native packet copy           | GENEVE encapsulated forwarding    |
| **Routing impact**     | None                         | Requires routing through GWLB     |
