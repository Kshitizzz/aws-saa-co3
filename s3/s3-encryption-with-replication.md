# S3 Replication and Encryption (SSE-KMS + Multi-Region KMS Keys)

## Memory Hook
- “Encrypted data still needs permissions to replicate”
- “KMS key in one region ≠ valid in another unless it's an MRK”

---

## ✅ Core Concepts: How S3 Replication Handles Encrypted Data

| Encryption Type   | Replication Supported? | Notes                                                 |
|--------------------|------------------------|--------------------------------------------------------|
| SSE-S3             | ✅ Yes                 | Transparent replication — no extra config needed       |
| SSE-KMS (same-region key) | ✅ Yes         | Requires IAM + KMS permissions in both source + dest   |
| SSE-KMS (multi-region key) | ✅ Yes        | Simplifies permissions and allows seamless replication |
| SSE-C              | ❌ No                  | AWS cannot decrypt — so cannot replicate               |

---

## 🔐 KMS Permission Requirements

### For SSE-KMS + CRR (Cross-Region Replication)

| Region           | Required IAM Permissions           |
|------------------|-------------------------------------|
| **Source Region** | `kms:Decrypt` on the source KMS key |
| **Destination**   | `kms:Encrypt` on the dest KMS key   |

🧠 Without these, replication will silently fail for encrypted objects  
🧠 These are **not the same** as standard S3 access permissions

---

## 🌍 Multi-Region KMS Keys (MRKs)

> A **Multi-Region KMS key** is a special KMS key that you can **replicate across regions**, but manage as a single logical key pair.

### Benefits:
- KMS key in Region A ≈ key in Region B (but physically separate)
- Compatible with:
  - **S3 CRR**
  - **Lambda**
  - **EBS snapshots**

### MRK Key IDs are:
- **Different per region**
- But **share the same key material + logical ID**

---

## 🧠 S3 Replication with MRKs – Why It Matters

| Use Case                             | Why MRK Helps                                |
|--------------------------------------|-----------------------------------------------|
| Replicate encrypted data cross-region| Simplifies encryption + replication setup     |
| Avoid KMS permission errors          | MRKs have identical policies + trust config   |
| Minimize latency on decrypt in dest  | MRK is region-local → better performance      |

---

## ✅ Sample S3 Replication + SSE-KMS Flow

1. Object uploaded in Region A, encrypted with SSE-KMS
2. S3 triggers CRR
3. S3 **decrypts object using source KMS key (needs `kms:Decrypt`)**
4. S3 **re-encrypts with destination KMS key (needs `kms:Encrypt`)**
5. Object stored in destination bucket

💡 With **MRK**, step 3 & 4 are seamless because key trust + policy is aligned

---

## ⚠️ Gotchas

- S3 **does not replicate KMS keys** themselves — you must create the key in each region
- **You must explicitly grant S3** the required `kms:*` permissions for replication to work
- Enabling SSE-KMS **after enabling replication** won’t retroactively apply permissions

---

## 📌 Exam Pointers

- “Replication fails with SSE-KMS encrypted objects?” → ✅ Check for `kms:Decrypt`/`Encrypt` perms
- “How to simplify cross-region encryption handling?” → ✅ Use Multi-Region KMS keys
- “Can AWS replicate SSE-C encrypted data?” → ❌ No
- “Does replication carry over the same KMS key ID?” → ❌ No — key ID is different per region, even for MRKs

---

## 🛠️ Best Practices

- ✅ Always pre-create the KMS key in both regions before enabling CRR
- ✅ Use **MRK** if regulatory compliance allows (simplifies lifecycle)
- ✅ Add `aws:sourceVpce`, `aws:PrincipalOrgId` to bucket policy if needed
- ✅ Monitor replication failures in **S3 Replication metrics / CloudWatch**

