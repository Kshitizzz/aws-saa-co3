# S3 Cross-Region Replication with Different Encryption Models

## Memory Hook

- “CSE: Encrypt before you upload. SSE: Let S3 encrypt it for you.”
- “MRK = Universal decrypt badge across AWS regions.”

---

## Must-Know Core Concepts

### 1. S3 CRR with Client-Side Encryption (CSE) + MRK

- Data is encrypted on client-side using a DEK.
- DEK is itself encrypted using a KMS Multi-Region Key (MRK).
- Replicated encrypted data + encrypted DEK to target region.
- MRK allows the encrypted DEK to be decrypted in any region where MRK exists.
- **Use Case**: High control over encryption + seamless global decryption.

### 2. S3 CRR with SSE-KMS (Regional Key)

- S3 encrypts data using a regional KMS key in source region.
- Upon replication, destination S3 bucket must have **its own KMS key**.
- Re-encryption is performed using destination region key.
- ❌ Not automatically decryptable across regions.
- ✅ Requires key mapping and permissions in both regions.

### 3. S3 CRR with SSE-KMS + MRKs

- Both source and destination buckets use the **same MRK identity** (in different regions).
- On replication, S3 encrypts data at destination with local version of the MRK.
- ✅ Simplifies key management.
- ✅ Seamless access and decryption across regions.
- ✅ AWS Best Practice for secure CRR.

---

## Nuances & Edge Cases

- CSE = You manage encryption/decryption logic.
- SSE-KMS = S3 manages encryption using KMS CMKs.
- MRKs must be created explicitly in both regions — AWS doesn’t auto-replicate them.
- IAM permissions for KMS keys must be granted in both regions for CRR to succeed.
- In CSE, AWS never sees plaintext data — only you have decrypting capability.

---

## Exam Pointers

- **CSE + MRK** = Encrypt on client, decrypt anywhere (full control).
- **SSE-KMS + Regional Key** = Requires separate CMKs per region; complex.
- **SSE-KMS + MRK** = Seamless replication + secure; preferred for encrypted CRR.
- Know when to use each:  
  ➤ CSE for sensitive client-side logic  
  ➤ SSE for simplicity with MRK when multi-region is needed  
- MRKs = Key ID and key material same across regions — simplifies decryption.

