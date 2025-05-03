# IAM Final Concepts: Boundaries, Evaluation, Policy Types

## Memory Hook

- "IAM is like a club: users have memberships (policies), bouncers (evaluation logic) check the rules, and boundaries are the walls they can't cross—even if they have a VIP pass."
- Or
- "Permission Boundaries: 'You can go anywhere inside this fence—even if someone gives you a golden key.'"

## Must-Know Core Concepts

### 1. Permissions Boundaries

- Acts like a **maximum permission limit** for IAM roles or users.
- Even if a policy grants access, a boundary can block it.
- Often used in **delegation scenarios** — e.g., allowing a developer to create roles but only within defined limits.

**Exam Tip**: IAM boundaries don’t grant access—they restrict the scope.

### 2. IAM Policy Evaluation Logic

IAM decides **“Allow” or “Deny”** based on these rules:

| Step | Evaluation Rule                                                                 |
|------|----------------------------------------------------------------------------------|
| 1    | Check for **explicit deny** – takes priority over all                          |
| 2    | Check for **explicit allow** – if allowed, continue                            |
| 3    | If neither, **implicit deny** is applied                                       |
| 4    | **Permissions Boundaries** further restrict permissions (for users/roles only) |

**Exam Tip**: If permissions boundary blocks something, access is denied—even if the policy says “Allow”.

### 3. IAM Policy Types Recap

| Policy Type               | Applied To            | Purpose                                             |
|--------------------------|-----------------------|-----------------------------------------------------|
| **Identity Policy**       | Users, Groups, Roles  | Grants permissions                                  |
| **Resource-based Policy** | Resources (e.g., S3)  | Grants access to resources (often cross-account)    |
| **Permissions Boundary**  | Users, Roles          | Limits max permissions they can use                 |
| **Service Control Policy (SCP)** | AWS Accounts via Orgs | Defines guardrails (org-level max permissions)   |
| **Session Policy**        | Temporary Credentials | Further restricts permissions during STS sessions   |
| **Access Control List (ACL)** | Legacy (S3/others) | Low-level object permission control                |

## Nuances & Edge Cases

- If **either** a policy or a boundary denies access → **access is denied**.
- SCP + IAM Policy + Boundary = all must align to allow.
- Boundaries are **not commonly used** unless **delegation or custom roles creation** is in play.
- Session policies don’t override boundaries — they further **narrow access**.

## Best Practices & Exam Tips

- Always follow **least privilege** principle.
- Use **groups** + **identity-based policies** for scalability.
- Never use the **root account** — instead, enforce MFA on root.
- Know that **explicit deny** trumps all.
- Visualize IAM with the **policy evaluation flow**: Deny > Allow > Implicit Deny

