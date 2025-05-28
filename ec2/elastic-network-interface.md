# EC2 Networking – ENIs, IP Types & VPC Setup

## Memory Hook  
- “ENI = virtual NIC for EC2; EIP = static face on the public internet”  
- “Every EC2 lives in a subnet, every subnet lives in a VPC”

---

## ✅ Elastic Network Interfaces (ENIs)

> A virtual network card attached to an EC2 instance inside a **VPC**

### 🧩 ENI Components

| Attribute               | Description                              |
|--------------------------|------------------------------------------|
| **Primary private IP**   | Mandatory; assigned from subnet CIDR     |
| **Secondary private IPs**| Optional; used for multiple services     |
| **Elastic IP (EIP)**     | Optional; public IP mapped to private IP |
| **MAC address**          | Unique per ENI                           |
| **Security Groups**      | Attached to ENI                          |
| **Subnet binding**       | ENI is AZ-scoped                         |

---

### 💡 ENI Use Cases

- Attach multiple ENIs to one instance (multi-homing)
- Move ENIs across instances (failover or IP persistence)
- Assign multiple IPs to one ENI for load separation
- NIC-based firewalls (Security Groups are ENI-bound)

---

## 🧠 ENI Types

| Type                 | Description                                               |
|----------------------|-----------------------------------------------------------|
| **Primary ENI**       | Comes with EC2 by default                                |
| **Secondary ENI**     | Can attach up to limit (varies by instance type)         |
| **Trunk ENI**         | For **VPCs with VLAN tagging** (used in SDN setups)      |
| **Elastic Fabric Adapter (EFA)** | High-performance network card for HPC         |

---

## ✅ IP Address Types in EC2

### 🔹 Private IP (mandatory)

- Assigned from the subnet’s CIDR block
- Used for internal communication within VPC
- Can have multiple per ENI

### 🔹 Public IP (optional, dynamic)

- Assigned at launch if subnet allows `auto-assign public IP`
- Changes on stop/start
- NATed via AWS public network

### 🔹 Elastic IP (EIP) – static

- A **static public IPv4 address** you allocate
- Maps to a private IP on an ENI
- Survives instance stop/start
- Limited to **5 per account per Region (default)**

---

## 🧠 Elastic IP Use Cases

- DNS persistence for EC2 instances
- VPN endpoints, NAT Gateways
- Load balancer front-ends (when not using ALB/NLB DNS)

🧠 You’re **charged** if:
- EIP is not associated with a running resource
- You remap it more than 100 times/month

---

## 🔧 VPC Setup Summary (Context for EC2 Networking)

### VPC

- Logical isolation unit for your EC2
- Defines IP range via CIDR (e.g., `10.0.0.0/16`)
- Can span all AZs in a Region

### Subnet

- Subdivision of VPC
- Bound to one **Availability Zone**
- Can be **public** (has route to IGW) or **private** (no route to IGW)

### Routing

- **Route Table** controls traffic flow
- Default route `0.0.0.0/0` to IGW → public subnet
- No default route = isolated/private subnet

### Gateways

| Gateway             | Description                           |
|----------------------|----------------------------------------|
| **Internet Gateway (IGW)**     | Enables access to internet (public IP required) |
| **NAT Gateway**      | Enables **private subnet → internet** (outbound only) |
| **VPC Endpoints**    | AWS PrivateLink for internal AWS services access |

---

## 🔐 Security Behavior

| Layer             | Control Mechanism                            |
|--------------------|----------------------------------------------|
| Instance           | ✅ Security Groups (ENI-attached)            |
| Subnet             | ✅ NACLs (stateless firewall)                |
| VPC-wide traffic   | VPC Flow Logs (for visibility)              |

🧠 Security Groups = **stateful**, ENI-level  
🧠 NACLs = **stateless**, subnet-level

---

## 📌 Exam Pointers

- “Need a static public IP that survives EC2 restarts?” → ✅ Elastic IP
- “Attach multiple NICs to EC2 for traffic isolation?” → ✅ Use secondary ENIs
- “Restrict EC2 ingress traffic at instance level?” → ✅ Use Security Group
- “Route all outbound EC2 traffic in private subnet?” → ✅ NAT Gateway
- “Which AWS object has a private IP and EIP?” → ✅ ENI
- “What limits number of ENIs?” → ✅ EC2 instance type
- “Want to move IP from one instance to another?” → ✅ Detach ENI or remap EIP
