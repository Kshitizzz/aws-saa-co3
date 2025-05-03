# IAM Policies (AWS Identity & Access Management)

## Memory Hook

- "Policies = Permissions Blueprints"
- "Allow is a maybe, Deny is a hard NO"

## Must-Know Core Concepts

- IAM Policies are **JSON documents** used to allow or deny **permissions**
- Each policy contains:
  - `Effect`: Allow or Deny
  - `Action`: What operations (e.g., `s3:PutObject`)
  - `Resource`: Which resources
  - `Condition`: (Optional) fine-grained controls

## Types of Policies

- **Identity-based policies**: attached to users, groups, or roles
- **Resource-based policies**: attached to resources like S3, SNS, Lambda
- **Permissions Boundaries**: define max permissions a principal can have
- **Session Policies**: passed when assuming roles for temporary access
- **Service Control Policies (SCPs)**: org-level restriction (for Org setups)

## Inline vs Managed Policies

- **Inline**: tightly coupled, unique to one identity
- **Managed**:
  - AWS Managed: prebuilt, regularly updated
  - Customer Managed: reusable, user-controlled

## Nuances & Edge Cases

- **Deny always wins** over Allow
- **Policies are additive** unless a Deny exists
- IAM evaluates **all attached policies** together
- For resource-based policies, **no identity required** (e.g., public S3 access)
