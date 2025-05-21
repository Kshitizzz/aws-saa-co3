# Amazon S3 Encryption – SSE-S3, SSE-KMS, SSE-C, Client-Side

## Memory Hook  
- “SSE = AWS does encryption for you”  
- “CSE = You encrypt before upload”  
- “KMS = Keys with control”

---

## ✅ Types of S3 Encryption

| Type           | Full Name                              | Who Manages Key?     | Key Location     | TLS Required? |
|----------------|------------------------------------------|------------------------|------------------|----------------|
| **SSE-S3**     | Server-Side Encryption with S3-Managed Keys | AWS                   | Managed by S3     | ✅ Yes         |
| **SSE-KMS**    | Server-Side Encryption with KMS          | You (via KMS)         | KMS + S3          | ✅ Yes         |
| **SSE-C**      | Server-Side Encryption with Customer-Provided Keys | You                | Sent with request | ✅ Yes         |
| **Client-Side**| Client-Side Encryption (CSE)             | You                   | Outside AWS       | ❌ (TLS needed) |

---

## 🔐 SSE-S3

- Simplest encryption option  
- AWS handles key rotation + storage  
- Uses **AES-256 keys stored in S3**
- ✅ Zero config, enabled per PUT request or by default via bucket policy

**Use Case:** Basic compliance, internal workloads, no audit/control needed

---

## 🔐 SSE-KMS

- Uses **AWS KMS** to generate and manage keys  
- Adds **audit trail** via CloudTrail  
- Allows **per-object** and **per-user** key usage control
- Adds **KMS request quota + cost** (per API call)

**Use Case:** Regulated environments (HIPAA, PCI), fine-grained access control, multi-tenant logs

---

## 🔐 SSE-C

- You bring your own encryption key  
- AWS uses it **only for encryption at upload time**
- **Key never stored by AWS**
- Must supply the key with **every PUT/GET**

**Use Case:** You must manage keys outside AWS (regulated or air-gapped environments)

⚠️ AWS cannot recover the object if the key is lost

---

## 🔐 Client-Side Encryption (CSE)

- You encrypt data **before uploading to S3**
- S3 stores it as-is  
- You must **decrypt after download**
- Can use **AWS Encryption SDK**, **PGP**, **OpenSSL**, or 3rd-party libs

**Use Case:** BYOK systems, zero-trust storage, full end-to-end control

---

## 🧠 Encryption + Replication

| Encryption Type | Supported with CRR/SRR? | Notes                                      |
|------------------|-------------------------|---------------------------------------------|
| SSE-S3           | ✅ Yes                  | Transparent                                 |
| SSE-KMS          | ✅ Yes                  | Need `kms:Encrypt` in destination KMS key   |
| SSE-C            | ❌ No                   | AWS can't replicate as it can’t read the key |

---

## 📌 Exam Pointers

- “Need audit trail of encryption key usage?” → ✅ SSE-KMS
- “Compliance requires keys under customer control?” → ✅ SSE-C or Client-Side
- “How to encrypt uploads with zero setup?” → ✅ SSE-S3
- “Replication fails after enabling KMS?” → ✅ Add `kms:Decrypt` (source) + `kms:Encrypt` (dest)
- “Key is lost and object is unrecoverable?” → ✅ SSE-C or CSE

---

## 🛡️ Best Practices

- ✅ Use **SSE-KMS** for regulated workloads
- ✅ Use **default bucket encryption** to enforce at scale
- ❌ Do not use SSE-C unless you have very strong key management discipline
- ✅ Encrypt in transit using HTTPS always (TLS)

