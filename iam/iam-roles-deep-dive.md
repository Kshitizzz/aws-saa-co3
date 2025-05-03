# IAM Roles (Deep Dive)

## Memory Hook
- "Role = Uniform pehno, kaam karo, wapas do."
- "IAM user has an identity. IAM role **assumes** one temporarily."

---

## Must-Know Core Concepts

### What is an IAM Role?
- An IAM Role is **not a user**, it's an AWS identity **with specific permissions** that can be temporarily assumed.
- It has **no long-term credentials** like passwords or access keys.
- You can think of it like a **"temporary costume"** with powers (permissions) you wear for a specific task.

---

### Key Characteristics
- Roles are **assumed**, not logged into.
- The session is temporary (up to 12 hours max depending on config).
- Anyone or anything (user, service, app) can **assume a role** if allowed by a **trust policy**.
- Once assumed, a temporary **set of credentials** (AccessKey, SecretKey, SessionToken) is provided.

---

### When Are Roles Used?

| Scenario | Who Assumes the Role? | Why? |
|---------|------------------------|------|
| EC2 accessing S3 | EC2 Instance | Avoid hardcoding credentials |
| Lambda writing to DynamoDB | Lambda | Secure, temporary permissions |
| Cross-account access | User from Account A | Access resources in Account B |
| SSO Login (IAM Identity Center) | End-user | Temporary session with mapped permissions |
| AWS service assuming another role | Service | Perform actions on your behalf |

---

## Hinglish Explanation

- **IAM user** toh permanent aadmi hai — uske paas credentials hote hain, fixed identity.
- **IAM role** ek **temporary mask** hai — aap usse pehnte ho kaam ke liye aur baad mein utaar dete ho.
- Isme **long-term credentials nahi hote** — bas temporary tokens milte hain jab role assume kiya jata hai.
- Role kisi **service** (jaise EC2, Lambda), **user** ya **external user** (cross-account) ke liye banaya ja sakta hai.
- Jo role banata hai wo "trust policy" se batata hai ki **kaun us role ko assume kar sakta hai**.

---

## Trust Policy vs Permission Policy

- **Trust Policy** → Defines **who can assume** the role.
  - "Isko role use karne dena ya nahi?"
- **Permission Policy** → Defines **what the role can do**.
  - "Role assume karne ke baad ye kya-kya access kar sakta hai?"

---

## Types of IAM Roles

1. **Service Roles**  
   - AWS service assumes the role (e.g., EC2 → S3 access).

2. **Cross-Account Roles**  
   - Account A ka user, Account B ke resources access karta hai.

3. **Federated Identity Roles**  
   - External IdP (like Google or Azure AD) ka user assume karta hai via SAML or OIDC.

4. **IAM Identity Center Roles (Permission Sets)**  
   - IAM Identity Center assigns roles to users for AWS account access.

---

## Nuances & Edge Cases

- You cannot login to a role — you can **only assume it**.
- AWS CLI and SDK use `sts:AssumeRole` API to assume roles programmatically.
- Roles can be chained, but there are **STS session duration limits**.
- Each assumed role session gets a **session name** and **temporary credentials** — useful for auditing.

---

## Memory Hook (Reinforced)
- "Role = Temporary costume. Kaam khatam, costume wapas."
- "IAM user = aadmi; IAM role = kaam ke liye badalte roop."
