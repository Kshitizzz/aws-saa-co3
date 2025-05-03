# IAM Identity Center vs IAM Users & SCIM Provisioning

## Memory Hook

- "IAM users are local. Identity Center users are federated and scalable."
- "SCIM = Sync karo IdP se, manual work hatao."

---

## Must-Know Core Concepts

### IAM Users

- Created directly inside individual AWS accounts using IAM.
- Credentials: Console password + Access keys.
- Stored locally in the AWS account.
- Typically used for programmatic access or service accounts.
- **Not recommended for human access** in modern AWS environments.
- No central management across multiple accounts.

### IAM Identity Center Users

- Managed centrally via IAM Identity Center (formerly AWS SSO).
- Users can be created natively or synced from external Identity Providers (IdPs) like Okta, Azure AD.
- Uses **federated login**, not IAM credentials.
- Enables Single Sign-On (SSO) across multiple AWS accounts and external SaaS apps.
- Supports fine-grained permissions via permission sets.
- Recommended for human access — scalable, secure, and lifecycle-aware.

---

## SCIM Provisioning (System for Cross-domain Identity Management)

- SCIM is an open standard that automates user provisioning from external IdPs into IAM Identity Center.
- Used to synchronize:
  - User creation
  - Attribute updates (name, email, title, etc.)
  - Group membership
  - User deactivation/removal
- Reduces manual IAM Identity Center user management.
- Works with identity providers like:
  - Okta
  - Azure AD
  - Google Workspace
- Keeps user identity lifecycle in sync between your corporate directory and AWS.

---

## Nuances & Edge Cases

- IAM users still support long-term credentials — useful for automation or service accounts.
- IAM Identity Center **does not manage IAM users** — it’s a separate directory layer.
- SCIM only works if your IdP supports it and is connected correctly.
- You can assign access to both AWS accounts and **external applications** (SaaS apps) via Identity Center.
- Identity Center uses **permission sets**, not IAM policies directly — these map to IAM roles behind the scenes.

---

## Memory Hook (Reinforced)

- "IAM users = old-school, static, risky."
- "Identity Center = modern, federated, enterprise-ready."
- "SCIM = auto-sync karo, HR se leke AWS tak."
