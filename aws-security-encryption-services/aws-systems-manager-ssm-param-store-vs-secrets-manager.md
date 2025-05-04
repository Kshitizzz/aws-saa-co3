# AWS SSM Parameter Store vs Secrets Manager

## Memory Hook

- "Parameter Store = Notes app, Secrets Manager = Bank vault"
- Or
- "Use Parameter Store for configs, Secrets Manager for secrets"

## Must-Know Core Concepts

### ✅ AWS SSM Parameter Store

- Service to store config data and secrets as key-value pairs.
- Supports both plain text and encrypted values (via KMS).
- Two tiers:
  - **Standard** (free, limited throughput)
  - **Advanced** (paid, allows larger size and more history)
- Basic versioning and no built-in rotation.
- IAM used to control access to parameters.

### 🔐 AWS Secrets Manager

- Designed for **secure storage of secrets** like passwords, tokens, keys.
- Built-in support for **auto-rotation** using Lambda.
- Integrated with:
  - RDS, Redshift, DocumentDB for seamless credential rotation.
- Maintains **version history** and rich **CloudTrail logging**.
- More expensive than Parameter Store.

## Nuances & Edge Cases

- Parameter Store can store secrets, but lacks:
  - Native rotation
  - Rich versioning
  - Secret lifecycle management
- Secrets Manager encrypts every secret by default using KMS.
- Secrets Manager is a better fit for high-security and regulated environments.

## Exam Pointers

- 🛠 Use **Parameter Store** for general config and low-sensitivity values.
- 🔐 Use **Secrets Manager** for sensitive credentials with **auto-rotation**.
- 💸 Secrets Manager is **more expensive**, but has **richer features**.
- 🧩 Both integrate with **KMS**, **IAM**, and **CloudTrail**.
- ❗ Only **Secrets Manager** has built-in Lambda-based secret rotation.
