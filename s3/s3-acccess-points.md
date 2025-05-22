# Amazon S3 Access Points

## Memory Hook  
- “Different entry gates to the same warehouse”
- “Bucket stays private, access points open doors with rules”

---

## ✅ What Are S3 Access Points?

An **S3 Access Point** is a **named network endpoint** attached to an S3 bucket, each with:
- Its own **policy**
- Optional **VPC restriction**
- Unique DNS name

> Think of it like creating **custom doors into a shared S3 bucket**, each with its **own rules**

---

## 🔧 Why Use Access Points?

| Challenge                             | Access Point Benefit                               |
|--------------------------------------|----------------------------------------------------|
| Too many complex IAM/bucket policies | ✅ Simplify access per team/app                     |
| Need per-VPC data control            | ✅ Restrict access to S3 from within a VPC only     |
| Want to decouple IAM logic           | ✅ Each access point has its own access policy      |
| Multi-tenant bucket design           | ✅ Use different access points for different apps   |

---

## 🔐 Access Point DNS Format

- https://<access-point-name>-<account-id>.s3-accesspoint.<region>.amazonaws.com
- ✅ This DNS name is used **instead of the bucket name**

---

## 🧠 Key Properties

| Property              | Description                                           |
|-----------------------|-------------------------------------------------------|
| **1 bucket = many access points** | Each with distinct policies and controls |
| **Name-scoped globally**         | Unique per AWS account + region            |
| **Access via SDKs/CLI supported**| Must use correct access point ARN/DNS     |
| **IAM or resource-based policy** | Either can govern permissions             |
| **Supports VPC-only access**     | With VPC-access mode (interface endpoint) |

---

## 🚧 Access Points vs Bucket Policies

| Feature                  | Bucket Policy                   | S3 Access Point Policy                |
|--------------------------|----------------------------------|---------------------------------------|
| Scope                    | Entire bucket                   | Scoped to a specific access point     |
| Useful for               | Global/default policies         | Application-specific use cases        |
| Complexity               | Can grow complex over time      | Simpler, focused per consumer         |
| VPC restriction?         | ❌ Not natively                  | ✅ Yes                                 |

---

## 🧪 Use Case Examples

- A **central data lake bucket** accessed by:
  - BI team via one access point (read-only)
  - ETL jobs via another (read + write)
  - ML training in VPC via VPC-restricted access point

- Access S3 **only from specific VPCs** without exposing public bucket policies

---

## 🧠 VPC-Only Access Points (Interface-Enabled)

- Can be made **VPC-restricted** using **VPC Endpoints**
- Use **interface-style access point** via `s3-accesspoint.region.amazonaws.com`
- **Great for private data lakes, analytics jobs, cross-account setups**

---

## 📌 Exam Pointers

- “How to allow app A read-only access, app B full access to the same bucket?”  
  → ✅ Use separate S3 Access Points with unique policies

- “How to enforce private access to S3 from only inside a VPC?”  
  → ✅ Use a VPC-restricted access point + S3 bucket with `aws:sourceVpce`

- “Can one bucket have multiple access points?”  
  → ✅ Yes

- “Do access points expose full bucket access?”  
  → ❌ No — limited by policy attached to the access point

- “Do access points work with cross-account permissions?”  
  → ✅ Yes — use ARNs with `s3:AccessPointArn`

---
