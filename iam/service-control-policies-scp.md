# Service Control Policies (SCPs)

## Memory Hook

- "IAM decides **who** can do what, SCPs decide **whether** it’s even allowed at all."
- Or: "SCPs = Org-level permission ceilings."

## Must-Know Core Concepts

- SCPs are **guardrails** used in AWS Organizations to define **maximum available permissions** for AWS accounts.
- They **do not grant permissions**, only **limit** them.
- Applied to:
  - AWS Organization root (entire org)
  - Organizational Units (OUs)
  - Individual member accounts
- SCPs affect **only IAM identities (users, groups, roles)** within member accounts. **Not the management account** itself.
- For any action to be allowed:
  - **Allowed by SCP**
  - **Allowed by IAM policy**
  - No explicit deny anywhere

## Nuances & Edge Cases

- SCPs default to **allow everything** (if no SCP is attached).
- Explicit `Deny` in SCP overrides all other permissions.
- Even Admins with `AdministratorAccess` won't be able to do something if SCP blocks it.
- You can attach **multiple SCPs** to an OU or account — result is the **intersection** (i.e., least privilege).
- To restrict actions (like disabling CloudTrail or deleting S3), use an SCP deny policy.

## Common Use Cases

- Prevent S3 bucket deletion across all accounts.
- Block usage of expensive services like EC2 GPU instances.
- Limit AWS Regions accessible (e.g., deny everything outside `us-east-1`).
- Ensure security tools like GuardDuty, Config, or CloudTrail can’t be turned off.

## Example SCP Policy (deny S3 delete):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:DeleteBucket",
      "Resource": "*"
    }
  ]
}
