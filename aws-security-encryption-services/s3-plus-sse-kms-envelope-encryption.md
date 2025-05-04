# S3 + SSE-KMS + Envelope Encryption

## Memory Hook

- "S3 khud encryption karta hai, KMS sirf chaabi deta hai."
- "DEK se data encrypt, CMK se DEK encrypt — that's envelope encryption."

## Must-Know Core Concepts

- SSE-KMS (Server Side Encryption with KMS) is an option in S3 where AWS KMS manages encryption keys.
- S3 doesn't send the object directly to KMS.
- Instead, S3:
  - Calls KMS to get a **Data Encryption Key (DEK)** using the `GenerateDataKey` API.
  - Uses **plaintext DEK** to encrypt the object.
  - Stores the **encrypted DEK** (ciphertext blob) alongside the encrypted object.
- During download (GET), S3:
  - Retrieves the encrypted DEK.
  - Calls KMS to decrypt it.
  - Uses the decrypted DEK to decrypt the object before sending it to the requester.

## Nuances & Edge Cases

- The plaintext DEK is never stored; only held temporarily in memory.
- KMS logs every call to `GenerateDataKey`, `Decrypt`, etc. to CloudTrail.
- Authorization to use CMKs is controlled via IAM and KMS key policies.
- CMKs used in SSE-KMS are **regional**, not global.
- SSE-KMS provides auditability and tighter access control than SSE-S3.
- Cost: Every `GenerateDataKey` and `Decrypt` is a paid KMS request.

## Exam Pointers

- SSE-KMS uses **envelope encryption**.
- Data is encrypted in S3; **KMS does not see the data itself**.
- You can enforce use of SSE-KMS using S3 bucket policies.
- You must have KMS permissions (`kms:GenerateDataKey`, `kms:Decrypt`) to use the CMK.
- Key rotation is available for CMKs and can be automatic.
- KMS is a **regional service**; keys do not replicate across regions.
