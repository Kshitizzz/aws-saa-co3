## IAM + Encryption Linkage

- IAM policies + KMS Key policies jointly control access.
- Encryption adds extra **authorization checks**.
- Cross-Region Replication with SSE-KMS needs correct IAM and KMS permissions:
  - Replication Role must have KMS access for both regions.
- Without correct permissions:
  - Uploads fail
  - Downloads fail
  - Replication silently fails

---

## Nuances & Edge Cases

- SSE-KMS requests are logged in CloudTrail (audit-friendly).
- SSE-KMS allows using MRKs for cross-region support.
- Default encryption can be set per bucket.
- Permissions need to be aligned across IAM & KMS key policies.

---

## Exam Pointers

- SSE-S3 = Simple, no IAM overhead.
- SSE-KMS = More secure, but needs detailed IAM + KMS permissions.
- SSE-C = Advanced, not recommended unless you control keys tightly.
- Know how IAM, bucket policies, and KMS key policies intersect.
- In CRR + SSE-KMS:
  - Source region: `kms:Decrypt`
  - Destination region: `kms:Encrypt`

