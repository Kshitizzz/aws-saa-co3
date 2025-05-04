# DynamoDB Global Tables & KMS Multi-Region Keys (CSE)

## Memory Hook

- "Global Tables = DynamoDB goes international."
- "Multi-Region KMS = Same key identity, different regions — like twins with the same brain."

---

## Must-Know Core Concepts

### DynamoDB Global Tables

- Fully managed, multi-region, multi-active replication.
- Each region has full read/write capabilities.
- Changes made in one region are replicated across others automatically.
- Helps reduce latency for globally distributed applications.
- Built-in conflict resolution (last writer wins).
- Use cases: Gaming leaderboards, user profile sync, global fintech apps.

### AWS KMS Multi-Region Keys (MRK)

- MRKs are symmetric CMKs that are created in multiple AWS regions but share the same key material and key ID.
- Each key in different region is an independent KMS resource but logically part of one MRK set.
- Supports use cases where encrypted data is moved across regions (e.g., S3 replication, DynamoDB Global Tables).
- Reduces complexity in key management for multi-region apps.

### Client-Side Encryption (CSE)

- Data is encrypted before sending to AWS services like S3, DynamoDB.
- Application requests AWS KMS to generate a DEK (Data Encryption Key).
- App encrypts data using DEK, stores encrypted data, and encrypted DEK alongside.
- In a multi-region setup, MRKs ensure consistent encryption/decryption across regions.

---

## Nuances & Edge Cases

- Conflict resolution in Global Tables is eventual consistency based (last writer wins).
- MRKs are not automatically replicated — you must manually replicate them when creating.
- Not all KMS features are available for MRKs (e.g., custom key stores not supported).
- MRKs cost slightly more due to cross-region capability.

---

## Exam Pointers

- DynamoDB Global Tables support **multi-master**, **multi-region** writes.
- For cross-region encryption/decryption, use **KMS Multi-Region Keys**.
- CSE shifts encryption responsibility to client code — AWS never sees your plaintext.
- Understand the **difference between regional CMKs and MRKs**.
- Expect scenarios around latency, DR, or compliance where MRKs and Global Tables are ideal.
