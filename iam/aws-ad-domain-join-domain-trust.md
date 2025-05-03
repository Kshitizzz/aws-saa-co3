## Domain Join (EC2 Instances)

### What does it mean?

- Domain joining means your EC2 instance becomes part of a **Windows domain**.
- After domain join, EC2 can be:
  - Managed using **Group Policies**.
  - Logged into using **domain credentials**.
  - Tracked centrally by your **Active Directory**.

### How is it done?

- Use **SSM or EC2 launch settings** to join domain on boot.
- Requires **connectivity** to your directory (via VPC or Direct Connect if on-prem).

---

## What is Domain Trust?

### Definition

- A **trust relationship** allows **users in one domain** to **access resources in another domain**.
- Think of it as **"I trust your users enough to let them in."**

### AWS Relevance

- **Only AWS Managed Microsoft AD** supports domain trust.
- Typical use: You have **on-prem AD** and want **AWS-hosted workloads** to trust on-prem identities without duplication.

### Trust Types

- **One-way trust**: Only one direction allowed.
- **Two-way trust**: Both domains accept each other’s users.

---

## Hinglish Explanation

- AWS Managed Microsoft AD → Full VIP solution hai. Apna **khud ka domain**, apni users list, trust bhi kar sakta hai dusri domains se.
- AD Connector → Apna AD already hai on-prem? Bas AWS pe **signal forward karne wala bandha** chahiye. Ye wahi hai.
- Simple AD → Cheap version hai. Dev/test ke liye theek hai, lekin enterprise-level features nahi milte.
- Domain join matlab EC2 ko bolna: “Ab tu hamari company ka hai. Login bhi domain ke users se hoga, aur policies bhi lagegi.”
- Trust matlab: “Main teri company ke logon ko bhi access dene ko ready hoon, bas mutual trust hona chahiye.”
