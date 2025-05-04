# AWS Key Management Service (KMS)

## Memory Hook
- “KMS = Your Key, Their Vault. Encrypt smart, sleep well.”
- “AWS KMS – Handle keys like secrets, not spaghetti code.”

## Must-Know Core Concepts
- AWS KMS is a **managed service** that enables you to create and control encryption keys.
- It is integrated with over 100 AWS services to encrypt data at rest and in transit.
- KMS supports both **symmetric** and **asymmetric** keys:
  - **Symmetric** (same key to encrypt/decrypt) – Default.
  - **Asymmetric** (public/private key pair) – For digital signatures, encryption.
- **Customer Master Keys (CMKs)**:
  - **AWS-managed CMKs**: Automatically created, minimal control.
  - **Customer-managed CMKs**: Full control, rotation, IAM & key policies.
- **Envelope Encryption**:
  - Data is encrypted using a data key.
  - The data key itself is encrypted using the CMK in KMS.
- Supports **automatic key rotation** (every 365 days) for customer-managed CMKs.
- **Audit Logs** available via CloudTrail for key usage and access.

## Nuances & Edge Cases
- Default service keys (AWS-managed) cannot be deleted or rotated manually.
- KMS has **per-request quotas** (transactions per second), especially relevant for high-volume apps.
- KMS doesn’t store actual data—only the keys and their usage policies.
- Regional Service: Keys do not replicate across regions (unless custom replication is built).
- **Key policy vs IAM policy**: Both can control access. The most restrictive one applies.
- Use **Grants** for temporary key permissions (alternative to changing key policies).

## Exam Pointers
- Know the difference between **AWS-managed CMK** and **Customer-managed CMK**.
- **Envelope encryption** will often appear in scenario questions.
- **Automatic key rotation** only applies to customer-managed CMKs.
- Expect scenario-based questions with **CloudTrail logging**, **access control**, and **encryption across services** (S3, EBS, etc.).
- Remember: KMS is **regional**, and keys do not auto-replicate.
