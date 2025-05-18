# AWS Gateway Comparison – VGW vs TGW vs DXGW vs Others

## Memory Hook

- “VGW = One VPC”
- “TGW = Many VPCs”
- “DXGW = Global DX Hub”
- “IGW/NAT = Internet doorways”
- “GWLB = Security traffic redirector”

---

## ✅ Core Comparison Table

| Gateway Type       | Purpose                                          | Scope         | Supports VPN | Supports DX | VPC Sharing | Transitive Routing |
|--------------------|--------------------------------------------------|---------------|--------------|-------------|--------------|---------------------|
| **VGW**            | VPN/DX termination point for one VPC             | VPC-level     | ✅ Yes       | ✅ Yes (via Private VIF) | ❌ No         | ❌ No              |
| **TGW**            | Hub for VPC-to-VPC and VPN/DX connectivity       | Regional      | ✅ Yes       | ✅ Yes (Transit VIF) | ✅ Yes (many) | ✅ Yes              |
| **DXGW**           | Global DX routing hub to multiple VGWs/TGWs      | Global        | ❌ No        | ✅ Required         | ✅ Yes         | ❌ No (point-to-point only) |
| **IGW**            | Internet access (inbound/outbound)               | VPC-level     | ❌ No        | ❌ No               | ❌ No         | ❌ No              |
| **NAT Gateway**    | Outbound-only internet for private subnets       | Subnet-level  | ❌ No        | ❌ No               | ❌ No         | ❌ No              |
| **EOIGW**          | IPv6-only egress for private subnets             | VPC-level     | ❌ No        | ❌ No               | ❌ No         | ❌ No              |
| **GWLB**           | Inline traffic forwarding to security appliances | Subnet-level  | ❌ No        | ❌ No               | ✅ Via service VPC | ❌ No              |

---

## 🧠 Notes on Key Gateways

### 🔹 Virtual Private Gateway (VGW)
- Used to **terminate Site-to-Site VPN or DX**
- **One VPC only**
- Provides **two VPN tunnels** for HA (not aggregateable)

---

### 🔹 Transit Gateway (TGW)
- Acts as a **central router/hub**
- Can connect:
  - ✅ Multiple VPCs
  - ✅ VPNs
  - ✅ Direct Connect
- Supports **transitive routing** and **routing tables**
- Supports **inter-region peering**

---

### 🔹 Direct Connect Gateway (DXGW)
- Global resource that **bridges DX to VGWs or TGWs**
- Required for **multi-region DX setups**
- No routing intelligence — you must connect it to TGW or VGW

---

### 🔹 Internet Gateway (IGW)
- Public subnet internet access
- Required for:
  - EC2 public IPs
  - ALB/ELB access from internet

---

### 🔹 NAT Gateway
- Enables **IPv4 outbound** internet for private subnets
- Stateless — doesn’t allow inbound connections
- Needs **EIP**

---

### 🔹 Egress-Only Internet Gateway (EOIGW)
- IPv6 version of NAT Gateway
- Outbound-only IPv6 traffic from private subnets
- No EIP or NAT needed

---

### 🔹 Gateway Load Balancer (GWLB)
- Passes traffic to **third-party firewall appliances**
- Works inline using **GENEVE encapsulation**
- Often used with **Network Firewall**, **IDS/IPS**, etc.

---

## 📌 Exam Pointers

- “Need to route VPN + VPC + DX with full control?” → ✅ Transit Gateway
- “Connect one DX circuit to 3 VPCs in 3 regions?” → ✅ DXGW + VGW/TGW
- “One VPN connection to one VPC?” → ✅ VGW
- “Want outbound-only internet for EC2 in private subnet?” → ✅ NAT Gateway
- “Need centralized inspection of traffic via firewall?” → ✅ Gateway Load Balancer

## [Extension] API Gateway 

## 🔹 API Gateway

| Property                     | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **Layer**                   | L7 (HTTP/S + WebSocket + REST)                                             |
| **Use Case**                | Securely expose backend APIs (Lambda, HTTP services, VPC services)         |
| **Scope**                   | Global (Edge-optimized), Regional, or Private                              |
| **Security Options**        | WAF integration, IAM auth, JWT, Lambda auth, Resource policies              |
| **Inbound/Outbound?**       | ✅ Inbound entry point (external to internal)                              |
| **VPC Integration?**        | ✅ Yes — via **VPC Link** (to connect to NLBs/private VPC services)         |
| **Transitive Routing?**     | ❌ No — it’s an **application layer proxy**, not a network router           |

---

## 📦 API Gateway in Context

| Gateway Type       | Traffic Level | Acts As                         | Common Integration            |
|--------------------|---------------|----------------------------------|--------------------------------|
| **API Gateway**    | L7 (HTTP/S)   | Public/Private API endpoint      | Lambda, HTTP backends, VPC Link |
| **IGW / NAT / EOIGW** | L3          | Internet connectivity            | EC2, NATGW, IPv6 egress         |
| **GWLB**           | L3/L4         | Traffic redirector (firewalls)   | Network Firewall, 3rd-party IPS |
| **TGW / DXGW / VGW** | L3 Routing   | Backbone routing layer           | VPN, DX, VPC interconnects      |

---

## 📌 Exam Pointers (API Gateway-specific)

- “Want to expose a Lambda via public HTTPS?” → ✅ Use API Gateway (regional or edge-optimized)
- “Secure API endpoint with WAF + custom auth?” → ✅ Use API Gateway + WAF + Cognito or IAM
- “Connect private ALB in VPC to public API Gateway?” → ✅ Use **VPC Link** with API Gateway
- “Do I need IGW for API Gateway?” → ❌ No — it's fully managed and globally reachable unless private

