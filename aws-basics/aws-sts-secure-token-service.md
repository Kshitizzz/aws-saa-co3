# AWS Security Token Service (STS)

## Memory Hook

- "STS = Security desk that hands out temporary badges for specific tasks"
- "Roles ride on STS."

## Must-Know Core Concepts

- AWS STS issues **temporary security credentials**
- Credentials include:
  - `AccessKeyId`
  - `SecretAccessKey`
  - `SessionToken`
- Commonly used with:
  - `AssumeRole`
  - `AssumeRoleWithSAML`
  - `AssumeRoleWithWebIdentity`
- Duration: 15 minutes to 12 hours (configurable)

## Use Cases

- **IAM Role assumption** (within or across accounts)
- **Federated access** (SSO using corporate identity provider)
- **Temporary elevated privileges**
- **Mobile or web apps** needing limited-time AWS access

## Nuances & Edge Cases

- Without the **SessionToken**, temporary credentials will not work — all three parts are mandatory.
- Temporary credentials can’t be manually rotated or extended — you must request new ones.
- STS is a **global service**, but some APIs can be **region-specific** (use regional STS endpoint when required).
