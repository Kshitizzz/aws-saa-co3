# Encrypted AMI Sharing in AWS

## Memory Hook

- "You can’t just share the AMI—share the keys too!"
- Or
- “Sharing an encrypted AMI? Don’t forget the padlock (KMS access)!”

## Must-Know Core Concepts

- An AMI encrypted using a **Customer Managed KMS Key (CMK)** can be shared across AWS accounts **only if** both the AMI and the **KMS key** used for encryption are shared properly.
- AMIs encrypted with **AWS-managed keys (e.g., aws/ebs)** **cannot** be shared across accounts.
- To share an encrypted AMI:
  - Share the AMI using `modify-image-attribute`
  - Share the **EBS snapshot** if AMI is EBS-backed
  - Modify the **KMS key policy** to allow the target account access
- Required KMS actions: `kms:Decrypt`, `kms:CreateGrant`, and `kms:DescribeKey`

## Nuances & Edge Cases

- Sharing the AMI without updating the KMS key policy will result in an `UnauthorizedOperation` error.
- If the snapshot is not shared, even with proper AMI and KMS permissions, the launch will fail.
- This process is **not needed for unencrypted AMIs**.
- KMS key policy must include the **account ID**, not just an IAM user or role.
- Works only with **customer-managed CMKs** — **default AWS-managed CMKs cannot be used** for cross-account sharing.

## Exam Pointers

- ❗ Must use **CMK** for encrypted AMI sharing — **default keys don't work**.
- 🔐 You need to grant the **target account** permission to use the CMK via **key policy**.
- 🧱 Share both the **AMI** and the **EBS snapshot**.
- 📑 Key policy must allow `kms:Decrypt`, `kms:CreateGrant`, and `kms:DescribeKey`.
- 💥 AMI sharing fails silently or throws `UnauthorizedOperation` if permissions aren't properly set.

