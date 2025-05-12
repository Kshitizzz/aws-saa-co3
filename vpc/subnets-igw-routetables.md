# Public & Private Subnets, Route Tables, Internet Gateway

## Memory Hook
- “Public Subnet → Route to IGW”
- “Private Subnet → No route to IGW = no internet”

---

## ✅ Must-Know Core Concepts

### 📦 Subnet (Public vs Private)

| Type           | Route Table Has `0.0.0.0/0 → IGW`? | EC2 with Public IP? | Internet Reachable? |
|----------------|-----------------------------|----------------------|----------------------|
| **Public**     | ✅ Yes                        | ✅ Yes (or auto-assign) | ✅ Yes               |
| **Private**    | ❌ No IGW route               | Doesn’t matter       | ❌ No                |

- Subnet ≠ inherently public or private — it’s the **route table** that defines behavior.
- Multiple subnets can be in the same AZ with different use cases (e.g., frontend vs DB tier).

---

### 🌐 Internet Gateway (IGW)

- **Horizontally scaled**, redundant gateway attached to your VPC
- Provides **outbound and inbound** access to internet
- Must:
  - Be **attached to the VPC**
  - Have **route in the subnet’s route table**
  - Be used with **public IP** or **Elastic IP**

---

### 🛣️ Route Tables

- Each subnet is **explicitly associated** with **one route table**
- A route table has:
  - Local route (always there)
  - Optional internet route (`0.0.0.0/0 → igw-xyz`)
- You can:
  - Share one route table across subnets
  - Or isolate them with separate route tables

---

## ⚠️ Nuances & Gotchas

- Having an IGW **is not enough** — route table must point to it, and EC2 must have public IP.
- **Auto-assign public IP = disabled by default** in custom subnets.
- You can’t have **multiple IGWs per VPC**.
- Route table only applies to **outbound traffic** logic — **inbound is still controlled by SG/NACLs**.

---

## 🧪 Example Design

| Component               | Public Subnet           | Private Subnet        |
|--------------------------|--------------------------|------------------------|
| Route Table              | `0.0.0.0/0 → IGW`         | `0.0.0.0/0 → NAT GW`   |
| EC2 Auto-assign Public IP| ✅ Enabled                | ❌ Disabled            |
| IGW Connected            | ✅ Yes                    | ✅ Yes (but not used)  |
| Internet Reachable?      | ✅ Yes                    | ❌ (unless via NAT)    |

---

## 📌 Exam Pointers

- “App server in public, DB in private?” → ✅ Use separate subnets + route tables
- “EC2 has public IP but no internet access?” → ✅ Check if subnet has IGW route
- “Private subnet with internet access?” → ✅ Needs **NAT Gateway** (covered next)
- “How to define a public subnet?” → ✅ Subnet’s route table must have IGW route

