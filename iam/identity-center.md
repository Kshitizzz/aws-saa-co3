# IAM Identity Center (formerly AWS SSO)

## Memory Hook

- "One login, many accounts — IAM Identity Center is your master key."
- "IAM Identity Center = Smart HR manager for AWS users."

## Must-Know Core Concepts

- IAM Identity Center is a **centralized user access management** service for multiple AWS accounts and applications.
- It lets you define **users and groups** centrally and assign access to AWS accounts **without creating IAM users in each account**.
- Users log in via a **single sign-on (SSO) portal** and assume roles in target AWS accounts.
- **Permission Sets** define what access users have once they assume a role in an account.

## How It Works

- IAM Identity Center creates and manages **IAM roles** in target accounts.
- Users from Identity Center assume those roles when accessing accounts via SSO.
- You can use the **default internal directory**, or connect to an **external identity provider** (like Azure AD, Okta, etc.) via **SCIM**.
- Login happens through a **centralized web interface**, usually with multi-factor authentication (MFA).

## Directory Options

- **AWS Identity Center Directory** (default)
- **Active Directory (via AWS Directory Service)**
- **External Identity Provider (via SAML 2.0 or SCIM)**

## Nuances & Edge Cases

- IAM Identity Center users **do not exist in IAM** — they’re managed separately.
- Permissions are **attached to roles via Permission Sets**, not directly to users.
- SSO integration means **temporary credentials** are issued, enhancing security.
- You can configure MFA, session duration, and group-based access controls.
- Each AWS account has roles provisioned for access, but **Identity Center handles the role assumption automatically** for users.

## Exam Tips

- Know the difference between IAM users and Identity Center users.
- Remember that IAM Identity Center simplifies **multi-account access management**.
- Be aware of how **Permission Sets map to IAM roles**.
- Expect questions on **identity federation**, SCIM provisioning, and centralized access management.

## Memory Hook (repeat)

- "One login, many accounts — IAM Identity Center is your master key."
- "IAM Identity Center = Smart HR manager for AWS users."
