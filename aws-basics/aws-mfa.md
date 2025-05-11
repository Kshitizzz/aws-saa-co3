# AWS MFA (Multi-Factor Authentication)

## Memory Hook

- "Password is a lock. MFA is a deadbolt."
- "MFA = Extra padlock on your AWS door."

## Must-Know Core Concepts
- AWS MFA adds a **second layer of security** beyond username + password.
- Common MFA use cases include:
  - Console logins
  - CLI access (especially `sts:AssumeRole`)
  - Protecting sensitive operations (e.g. billing, resource deletion)
- Supported devices:
  - **Virtual MFA apps**: AWS Virtual MFA, Google Authenticator, Authy
  - **Hardware devices**: Physical keys from AWS
  - **U2F devices**: YubiKey and similar

## Nuances & Edge Cases
- Root user MFA is **highly recommended** — you cannot attach policies to root, so MFA is the only protection.
- IAM policies can enforce MFA usage using `aws:MultiFactorAuthPresent`.
- For CLI/SDK usage, MFA works via session tokens — user assumes a role after providing an MFA code to `sts:GetSessionToken`.
- MFA alone doesn’t authorize access — it **complements IAM policies**, not replaces them.
