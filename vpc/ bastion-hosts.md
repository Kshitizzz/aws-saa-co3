# Bastion Hosts in AWS

## Memory Hook
- “Bastion = Jump Gate to Your Private Fortress”
- “One secure path in, zero visibility out”

---

## ✅ Must-Know Core Concepts

- A **Bastion Host** is a hardened, public-facing EC2 instance in a **public subnet**
- Used to **securely SSH/RDP into private resources** in **private subnets**
- Acts as a “jump box” — only one point of administrative entry
- Private instances:
  - Have **no public IPs**
  - Are only accessible from **inside the VPC**

---

## 🔐 Security Setup

| Layer          | Best Practice                       |
|----------------|-------------------------------------|
| Security Group | Allow SSH (port 22) from your IP only |
| NACL           | Restrict to whitelisted source IP   |
| EC2 Setup      | Use strong SSH key, hardened AMI    |
| VPC Design     | Bastion in public subnet            |

---

## 🔄 Architecture Flow

1. Admin SSHs into **bastion host (public subnet)**  
2. From bastion, SSH into **private EC2 (private subnet)**  
3. No direct SSH/RDP allowed to private resources from internet  
4. Use **SSH agent forwarding** to keep keys off bastion (secure practice)

---

## 🧠 Bonus: Modern Bastion Alternatives

| Tool                     | Description                              |
|--------------------------|------------------------------------------|
| **SSM Session Manager**  | No bastion needed, direct shell access via IAM |
| **EC2 Instance Connect** | Browser-based, secure short-term SSH access |
| **VPN Gateway + NAT**    | For larger orgs with split tunnel VPN needs |

🧠 *SSM is preferred now — no open ports, no public IPs, IAM-controlled access.*

---

## 📌 Exam Pointers

- “How to securely SSH into private EC2?” → ✅ Bastion Host or ✅ SSM Session Manager
- “Which subnet should bastion host go into?” → ✅ Public subnet (with IGW)
- “How to harden bastion access?” → ✅ Restrict source IPs, use key-based auth
- “No SSH port open, but can still connect?” → ✅ Using **SSM Session Manager**

---

## ⚠️ Nuances & Gotchas

- Bastion host must have:
  - Public IP
  - Route to IGW
  - SG allowing SSH from admin IP
- Private instance must allow SSH **from Bastion’s private IP or SG**
- Bastion hosts should **not have access to the internet** beyond control plane
