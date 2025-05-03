# AWS Directory Services (Deep Dive)

## Memory Hook
- "AWS Directory Services = Cloud ka telephone directory for users & resources."
- "Teen types: AWS Managed AD, AD Connector, Simple AD — alag use-cases, alag setup."

---

## Must-Know Core Concepts

### ✅ Why Use Directory Services?
- Centralized **authentication** and **authorization** for users, groups, and resources.
- Integrates with **Microsoft Active Directory (AD)** – commonly used in enterprise environments.
- Enables:
  - Single Sign-On (SSO)
  - Domain joining of EC2 instances
  - Group-based access control
  - Integration with Microsoft services (like SharePoint, RDS SQL Server, etc.)

---

## The Three Types of AWS Directory Services

| Feature | AWS Managed Microsoft AD | AD Connector | Simple AD |
|--------|---------------------------|--------------|-----------|
| **Who manages AD?** | Fully managed by AWS | You manage on-prem AD | AWS hosts lightweight AD |
| **AD software** | Real Microsoft AD (Windows Server) | Proxy to on-prem AD | Samba-based AD |
| **Use case** | Full enterprise-grade AD in cloud | Use your existing AD | Lightweight, dev/test workloads |
| **Integration** | RDS SQL Server, EC2 join, SSO | EC2 domain join, SSO | EC2 domain join, basic apps |
| **Trust Relationships** | Supports domain trust | Uses existing trust in on-prem | No trust support |
| **Scalability** | Highly scalable (Multi-AZ) | Depends on on-prem AD | Limited to ~5,000 users |
| **AWS Region support** | Multi-AZ deployment | Connector must be placed in same VPC | Single AZ |
| **Pricing** | Higher (fully managed infra) | Low (no directory hosted in AWS) | Cheapest |

---

## 1. AWS Managed Microsoft AD

- **Fully managed, real Microsoft Active Directory.**
- AWS handles the domain controllers, replication, patching, monitoring.
- Can create **trust relationships** with your on-prem AD.
- Ideal for:
  - Enterprises with Windows-heavy infra
  - RDS SQL Server
  - EC2 domain join
  - Group policy management

### Exam Tip:
- Only option that supports **trust relationships** and **Microsoft AD schema extensions**.
- Runs in **Windows Server 2012 R2 or later**.

---

## 2. AD Connector

- **Does not host AD** — it's just a **proxy to on-premises Microsoft AD**.
- Useful for orgs that already have AD running on-prem and want to:
  - Let AWS apps (like WorkSpaces, EC2) **authenticate against on-prem AD**
  - Avoid syncing or duplicating directories

### Exam Tip:
- **No directory in AWS** — zero replication, no storage of user data.
- **Quickest setup** if you already have an AD and want to avoid migration.

---

## 3. Simple AD

- **Low-cost, lightweight directory** built on **Samba (open-source AD compatible)**.
- Suitable for:
  - Small teams
  - Dev/test environments
  - EC2 domain joining without heavy enterprise AD needs

### Limitations:
- Does not support trust relationships.
- Max ~5,000 users.
- Limited schema — won’t support apps needing full Microsoft AD.

### Exam Tip:
- Best for **cost-sensitive**, **non-production** workloads.
- **Don’t choose for enterprise features** — pick AWS Managed AD instead.

---

## Hinglish Deep Dive Summary

- **AWS Managed Microsoft AD** → "Poora ka poora Microsoft AD cloud mein, aur AWS isko chalata hai."  
  - Full enterprise setup. High cost, high integration.

- **AD Connector** → "Bridge jaisa hai — aapka existing on-prem AD ka use hota hai, AWS sirf connect karta hai."  
  - No replication, just passthrough proxy.

- **Simple AD** → "Chhota mota test/staging AD, Microsoft waala nahi, basic version hai."  
  - Cheap, limited use cases.

---

## Quick Exam Cracker Matrix

| Scenario | Pick This |
|---------|-----------|
| You want full AD in cloud | AWS Managed Microsoft AD |
| You already have on-prem AD | AD Connector |
| You want basic AD features for dev/test | Simple AD |
| You need trust relationships | AWS Managed Microsoft AD |
| You don’t want to manage any infra | AWS Managed Microsoft AD |
| You want lowest cost option | Simple AD |

---

## Memory Hook (Reinforced)
- **"Managed = AWS does everything."**
- **"Connector = Mere paas already AD hai."**
- **"Simple = Mujhe sirf basic test/dev chahiye."**
