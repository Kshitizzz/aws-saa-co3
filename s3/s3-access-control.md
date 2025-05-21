# Amazon S3 Access Control (ACLs, Bucket Policies, IAM, VPC)

## Memory Hook  
- “Who you are = IAM” (IAM User) 
- “What you own = Bucket Policy”  
- “Old school = ACL”  
- “Where you are = VPC restriction”

---

## ✅ IAM Policies (can be attached to IAM users, roles, groups to grant permissions on AWS resources)

| Scope        | Identity-based (attached to IAM users, roles, groups) |
|--------------|--------------------------------------------------------|
| Purpose      | Defines what an AWS identity **can do on any resource** |
| Structure    | JSON with `"Action"`, `"Effect"`, `"Resource"`         |

### Notes:
- IAM cannot restrict public access — only **controls AWS user/role access**
- Follows standard AWS evaluation logic: Deny > Allow > Default Deny

---

## ✅ Bucket Policies (can be attached to S3 buckets only defining who can access what in the bkt)

| Scope        | Resource-based (attached to **S3 bucket**)             |
|--------------|--------------------------------------------------------|
| Purpose      | Define who **outside the bucket** can access objects (priciples include other AWS services too)|
| Structure    | JSON with `"Principal"`, `"Action"`, `"Resource"`      |

### Highlights:
- Can allow **cross-account access** (mention cross account AWS ID in the bucket policy)
- Can restrict access by:
  - IP (`aws:SourceIp`)
  - VPC (`aws:SourceVpc`)
  - VPC Endpoint (`aws:sourceVpce`)
- Can **deny all except a specific condition**

## Best Practise 
- is to use combo of both IAM policies and bucket policies to restrict access 

---

## ✅ Object ACLs (Access Control Lists)

| Scope        | Legacy feature (per-object or per-bucket level)       |
|--------------|--------------------------------------------------------|
| Purpose      | Grant **public access**, or cross-account object-level perms |
| Granularity  | Finer than bucket policy — works on individual object  |

- diff between Object ACLs and Bucket Policies is the ACLs can provide public access at an object level 
- while a bucket policy can only enforce what a principle (IAM resources such as Users, Roles, Groups can do in the bucket - can access what in the bucket)

### Notes:
- Only needed for **legacy apps** or **cross-account uploads**
- ACLs can be disabled by enabling **Bucket Ownership Enforcement**

---

## ✅ VPC-Based Access Control

| Feature                | What it Does                                 |
|------------------------|-----------------------------------------------|
| **S3 Bucket Policy + SourceVpc**   | Restrict access to requests from a specific VPC |
| **S3 Bucket Policy + SourceVpce**  | Restrict access to requests via specific **VPC Endpoint** |

🧠 Used to enforce **private network access** to S3 only (no public internet)

---

## 🔒 Best Practices

- ✅ Enable **Block Public Access** (default for new buckets)
- ✅ Use **Bucket Policies** for resource protection
- ✅ Use **IAM for identity permissioning**
- ❌ Avoid ACLs unless absolutely required (when you wanna define public access at an object level)
- ✅ Combine Bucket Policy + VPC Endpoint for airtight security

---

## 🧠 Evaluation Order Summary

1. Block Public Access settings (if on, it overrides everything)
2. IAM Policy (identity-level permissions)
3. Bucket Policy (resource-level permissions)
4. ACLs (only if not disabled)
5. Explicit Deny beats everything

---

## 📌 Exam Pointers

- “How to allow access from specific VPC endpoint?” → ✅ Use Bucket Policy with `aws:SourceVpce`
- “User has IAM allow, but still denied?” → ✅ Check bucket policy or Block Public Access
- “Want to block all except trusted AWS Org?” → ✅ Use `aws:PrincipalOrgId` in Bucket Policy
- “Need to allow S3 access without public internet?” → ✅ Use VPC Endpoint + Restrictive Bucket Policy
- “Need to give cross-account access to upload?” → ✅ Use Bucket Policy or Object ACL

