# Default VPCs, Subnets, Route Tables, and IGW

## Memory Hook

- “Default VPC = Instant plug-and-play network”
- “Works out of the box for EC2, but not for production!”

---

## ✅ Must-Know Core Concepts

### 📦 Default VPC

- Created automatically **per region**
- CIDR block: `172.31.0.0/16`  
- Can be deleted (but not auto-recreated unless you manually restore)
- Default VPC supports:
  - EC2, RDS, Lambda, etc.
  - Internet access via default setup

---

### 🧩 Default Subnets

- One **default subnet per AZ** (e.g., `/20` size)
- Auto-assigned **public IPs** to EC2 instances
- Each subnet is **public** by default (has route to Internet Gateway)

---

### 🛣️ Default Route Table

- Automatically associated with all default subnets
- Has this route by default:  
  `0.0.0.0/0 → Internet Gateway`
- You can modify/add more rules (e.g., route to NAT)

---

### 🌐 Default Internet Gateway (IGW)

- Automatically attached to the default VPC
- Enables internet access for all default subnets
- Works **only** if:
  - Subnet route table allows `0.0.0.0/0`
  - EC2 has public IP

---

## ⚠️ Nuances & Edge Cases

- You can **create a new default VPC** using `ec2 create-default-vpc` CLI
- You cannot **manually label** a VPC as "default" — AWS decides that
- If you delete default VPC and create custom one:
  - EC2 wizards will **not auto-assign public IPs**
- You can **customize or detach IGW**, but then subnet won’t be public anymore

---

## 📌 Exam Pointers

- “Why does EC2 launch with public IP by default?” → ✅ It's in **default subnet**
- “Want to restore default networking setup?” → ✅ Use `create-default-vpc`
- “EC2 has public IP but no internet access?” → ✅ Check route table → IGW missing?
- “What’s the default VPC CIDR?” → ✅ `172.31.0.0/16`

---

## 🧠 Summary

| Component      | Default Behavior                                         |
|----------------|----------------------------------------------------------|
| VPC            | One per region, `172.31.0.0/16` CIDR                     |
| Subnets        | One per AZ, public, auto-assign public IPs              |
| Route Table    | Routes `0.0.0.0/0` to IGW                                |
| Internet GW    | Attached to VPC by default                              |
