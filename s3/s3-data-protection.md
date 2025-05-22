# Amazon S3 Data Protection Features

## Memory Hook  
- “Durable by design, but protect from yourself”
- “S3 saves your data — unless you tell it to delete it twice”

---

## ✅ 1. Durability and Availability

| Feature        | Value                                |
|----------------|----------------------------------------|
| **Durability** | 99.999999999% (11 9s)                 |
| **Availability** | 99.99% (Standard)                    |

### Key Insight:
- S3 **automatically replicates data across multiple AZs**
- Durable ≠ Recoverable if you delete intentionally or overwrite data

---

## ✅ 2. Versioning

- **Protects against accidental deletes and overwrites**
- Each `PUT`, `DELETE`, or overwrite creates a new version
- Delete = **adds a delete marker**, not actual deletion
- Previous versions can be recovered manually

---

## ✅ 3. MFA Delete

- Adds a layer of protection for **versioned buckets**
- Requires:
  - **MFA device + token**
  - For DELETE of versioned objects or disabling versioning

### How to Enable:
- Must be enabled via **CLI or API** (not console)
- Applies to **bucket owners only**

### Limitation:
- ❌ Not supported for cross-account deletes  
- ❌ Not supported with lifecycle rules

---

## S3 Glacier Vault Lock

- Protects a bucket from deletion / overwrites on its objects.
- Applies lock at a bucket level to define that objects can't be deleted till a set period of time.
- Can define retention periods
- This is applied at the **bucket level**, precisely the diff between it and S3 object lock
- Needed for Write Once, Read Many (WORM) storage model for legal, compliance purpose.

## ✅ 4. S3 Object Lock

> Protect objects from deletion or overwrites for compliance use cases.

| Mode         | Behavior                                |
|--------------|------------------------------------------|
| **Governance** | Only privileged users can delete early |
| **Compliance** | **No one** can delete early (even root) |

- Works **with versioned buckets**
- Can define retention periods (e.g., 1 year immutability)
- Often used for **financial/legal archives**, WORM storage

---

## ✅ 5. S3 Replication (CRR/SRR)

- Acts as a **safety net** by copying objects to another bucket
- Replication is **asynchronous** and not retroactive
- ✅ Helps with **accidental deletes**, region loss scenarios
- ❌ Does not protect if **you delete both sides** (e.g., via lifecycle rule)

---

## ✅ 6. Block Public Access (BPA)

- A **top-level guardrail** against accidental public exposure
- Can be applied at:
  - Account level
  - Bucket level
- Blocks:
  - ACL-based public access
  - Bucket policy-based public access

---

## ✅ 7. S3 Access Logging

- Enables logs of every access request to your bucket
- ✅ Stored in another S3 bucket you control
- ✅ Use for audit, billing analysis, threat detection

---

## ✅ 8. CloudTrail Integration

- Logs all **S3 API calls** at the account level
- ✅ Includes `PUT`, `DELETE`, `LIST`, `GET`
- ✅ Essential for **audit trails and incident response**

---

## 📌 Exam Pointers

- “How to prevent accidental deletion?” → ✅ Enable versioning
- “Want to enforce WORM data retention?” → ✅ Use S3 Object Lock in Compliance mode
- “Need to log all requests to bucket?” → ✅ Use S3 Access Logging
- “Need to protect against misconfiguring bucket policies?” → ✅ Enable Block Public Access
- “Who deleted an object last week?” → ✅ Check CloudTrail logs
- “Prevent deletion without MFA?” → ✅ Use MFA Delete (only via CLI/API)
