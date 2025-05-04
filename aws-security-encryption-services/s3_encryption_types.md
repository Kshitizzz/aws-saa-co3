# S3 Encryption Types + IAM Permissions

## Memory Hook

- “Encryption is useless without access control — IAM + KMS = gatekeepers.”
- “SSE-S3 is easy, SSE-KMS is secure, SSE-C is dangerous.”

---

## Must-Know Core Concepts

### SSE-S3 (S3 Managed Keys)

- Encryption: Handled by S3 automatically with AES-256.
- No need to manage or create KMS keys.
- IAM: No special permissions required.
- Use Case: Low security needs, cost-efficient.

### SSE-KMS (KMS Managed Keys)

- Encryption: Handled by S3 using a KMS CMK or MRK.
- You must specify the key (or default).
- IAM Permissions:
  - `kms:Encrypt`, `kms:Decrypt`, `kms:ReEncrypt*`
  - `kms:GenerateDataKey`, `kms:DescribeKey`
- Also ensure replication role has correct access on both source and destination keys in CRR setups.

### SSE-C (Customer Managed Keys)

- Encryption: Customer provides the key in headers.
- S3 encrypts/decrypts but never stores the key.
- Risk: Exposes key in transit (must use HTTPS).
- IAM: No special permissions; access controlled by bucket policy.

---

