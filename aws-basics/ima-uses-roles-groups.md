# IAM Users, Groups, and Roles

## Memory Hook

- "User = Person, Group = Team, Role = Hat."
- "Users have logins. Roles are assumed. Groups assign shared power."

## Must-Know Core Concepts

- **IAM User**
  - Represents a **person or service** with a unique identity
  - Has long-term credentials: **password, access keys**
  - Can log in to the **AWS Management Console**, **CLI**, or **SDK**
  - Should be granted **least privilege**

- **IAM Group**
  - Collection of IAM users
  - Attach **policies** to groups for consistent permission management
  - Simplifies user permission management

- **IAM Role**
  - A set of temporary permissions that **can be assumed**
  - No login or credentials by default
  - Used by:
    - **AWS services** (e.g., EC2 instance accessing S3)
    - **Cross-account access**
    - **Federated users**
    - **Temporary tasks**

## Nuances & Edge Cases

- IAM users can **belong to multiple groups**, and receive cumulative permissions.
- Roles are **not assigned**, they are **assumed** temporarily using STS.
- You can **switch roles in the AWS Console** if your user is authorized to assume them.
- IAM roles are **best practice** for programmatic access — safer than long-term keys.

