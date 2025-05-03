# AWS Organizations – Centralized Account Management

## Memory Hook

- "One ring to rule them all — AWS Organizations ek boss account se baaki sab pe control deta hai."
- Or
- “Ek admin ka remote — sab accounts ka channel change wahi se hoga.”

## Must-Know Core Concepts

### ✅ What is AWS Organizations?

- Service to **centrally manage multiple AWS accounts** under a single umbrella.
- Use case:
  - Billing centralization
  - Apply policies (SCPs)
  - Manage account creation
  - Group accounts by purpose (e.g., dev, test, prod)

### ✅ Management Account

- The **first/root account** of the organization.
- Full control — can invite or create other accounts.
- Billing for all member accounts is consolidated here.

### ✅ Member Accounts

- The accounts that join the organization.
- Cannot leave or modify organization settings themselves.
- Follow rules/policies applied by the management account.

### ✅ Organizational Units (OUs)

- Logical grouping of accounts inside the org.
- Policies can be applied **to OUs**, and they inherit down to member accounts.
- Useful for structuring by **environment** or **department**.

### ✅ Consolidated Billing

- All accounts under org share **one bill**.
- No cross-account resource sharing, but **volume pricing discounts apply**.

### ✅ Service Control Policies (SCPs)

- Policies that define **maximum permissions** for accounts/OUs.
- They do **not grant** permissions — they only **restrict**.
- Attached at org root, OU, or individual account level.

## Nuances & Edge Cases

- SCPs apply only to **IAM identities (users, roles)** in member accounts — **not to root user** of those accounts.
- Even if IAM policy allows something, **SCP can block** it.
- If no SCP is attached, AWS treats it like **“allow everything”** by default.
- You can **deny use of specific regions or services** org-wide using SCPs.
- Organizations is a **global service**, just like IAM — no region boundaries.

## Real-World Analogy (Hinglish)

- Socho tumhara ek **parent account** hai (Management Account), uske under bacche accounts (Member Accounts) hain.
- Parent bolta hai — “Is ghar mein sirf 9 baje tak TV dekhne ki ijazat hai” → Baccha chahe jitna bhi chillaye, 9 ke baad TV band (SCP).
- Baccha apna remote (IAM policy) le aata hai, par SCP ka command zyada strong hai.

## Memory Hook

- "One ring to rule them all — AWS Organizations ek boss account se baaki sab pe control deta hai."
- Or
- “Ek admin ka remote — sab accounts ka channel change wahi se hoga.”
