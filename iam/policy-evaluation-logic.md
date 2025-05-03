# IAM Policy Evaluation Logic

## Memory Hook

- "By default, everything is denied. Allow only happens when granted explicitly. Deny is king."

## Must-Know Core Concepts

### IAM Evaluation Steps:

1. **Default Deny**: All requests are implicitly denied unless explicitly allowed.
2. **Explicit Deny Check**: If any policy explicitly denies the request, it overrides all allows.
3. **Evaluate Applicable Allows**: IAM then checks for explicit allow from:
   - IAM user/group/role policies
   - Resource-based policies
   - SCPs (in AWS Organizations)
   - Session policies (temporary credentials)

### If there is:

- **No Allow** → ❌ Denied
- **Allow only** → ✅ Allowed
- **Allow + Explicit Deny** → ❌ Denied

## Nuances & Edge Cases

- **Explicit Deny always wins**.
- **Service Control Policies (SCPs)** must also allow the action, else even valid IAM policies won’t work.
- **Multiple policies are merged** and evaluated together. Final decision is based on the combined result.

## Example:

If an IAM policy allows `s3:GetObject` on a bucket,
but the bucket policy explicitly denies `s3:GetObject` on one object:
→ ❌ Access is denied due to explicit deny.

## Memory Hook

- "IAM is paranoid. Denies first, allows second, but listens to Deny last."
