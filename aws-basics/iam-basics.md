# IAM Basics

## Memory Hook

* "IAM is the bouncer at the AWS club — who you are and what you’re allowed to do."
* Or
* "Identity & Access Management = Gatekeeper + Rulebook."

## Must-Know Core Concepts

* **IAM (Identity and Access Management)** lets you securely manage access to AWS services and resources.
* It controls **who** (identity) can **do what** (actions) on **which resources** under **what conditions**.
* IAM is **global**, not region-specific.

### IAM Components

* **Users**: Represents a single person or app with long-term credentials (username/password or access keys).
* **Groups**: A collection of IAM users. Policies attached to groups are inherited by users.
* **Roles**: Identities that can be assumed temporarily by trusted entities (users, services, accounts). Used for cross-account access, EC2 roles, etc.
* **Policies**: JSON documents defining permissions (Allow/Deny + Actions + Resources + Conditions).

### Policy Evaluation Logic

1. **Default Deny**: Everything is denied by default.
2. **Explicit Allow**: A policy must explicitly allow a request.
3. **Explicit Deny**: Overrides all allows. If any policy says Deny, it wins.

### Types of Policies

* **Managed Policies**:

  * *AWS Managed*: Created and maintained by AWS.
  * *Customer Managed*: Created and managed by you.
* **Inline Policies**: Directly embedded into a single user, group, or role.

### IAM Best Practices

* Follow **least privilege**: Grant only the permissions necessary.
* Use **IAM roles instead of users** for apps and services.
* Rotate credentials regularly, and enable **MFA (Multi-Factor Authentication)**.
* Use **IAM Access Analyzer** to review public/shared access.
* Never use the **root account** for daily tasks.

## Nuances & Edge Cases

* IAM is **eventually consistent** — policy changes can take a few seconds to apply.
* **Resource-level permissions** allow fine-grained access (e.g., specific S3 bucket, specific DynamoDB table).
* **IAM policies are not tied to regions** — but services like S3 or EC2 operate regionally.
* IAM is **free** — no cost for creating users, roles, or policies.
* IAM roles are preferred over long-term credentials for automation, cross-account, and EC2 access.

## Memory Hook (Repeat)

* "IAM is the bouncer at the AWS club — who you are and what you’re allowed to do."
* Or
* "Identity & Access Management = Gatekeeper + Rulebook."
