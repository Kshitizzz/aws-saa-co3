# IAM Role-Based vs Resource-Based Policies

## Memory Hook

- IAM Role-based = "Who can do what?"
- Resource-based = "Who can access me?"

## Must-Know Core Concepts

### Role-Based (Identity-Based) Policies

- Attached to: IAM Users, Groups, or Roles
- Define what **actions** the identity can perform on which **resources**
- Cannot directly grant cross-account access
- Common use case: EC2 instance role, Lambda execution role

### Resource-Based Policies

- Attached to: Specific AWS Resources (S3 buckets, Lambda, SQS, SNS, etc.)
- Define **who** (principals) can access the resource and **what actions** they can perform
- Can grant **cross-account access** directly
- Used for services that support sharing access

## Nuances & Edge Cases

- You can combine both: Role must be allowed via its IAM policy *and* resource must allow access via resource policy.
- Resource-based policies can include `Principal`, `Action`, `Effect`, `Condition`, etc.
- Only a few AWS services support resource-based policies.

## Example Resource Policy (S3):

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": {
      "AWS": "arn:aws:iam::111122223333:role/CrossAccountRole"
    },
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::example-bucket/*"
  }]
}
