# Security Groups vs NACLs

## Memory Hook
- “SG = Stateful, tight and polite”
- “NACL = Stateless, fast and furious”

---

## ✅ Core Comparison

| Feature               | **Security Group (SG)**                 | **Network ACL (NACL)**                   |
|-----------------------|-----------------------------------------|------------------------------------------|
| **Applies to**        | ENIs / EC2 / ALB                        | Subnet-level                             |
| **Traffic Type**      | Controls **inbound & outbound**         | Controls **inbound & outbound**          |
| **Stateful?**         | ✅ Yes — return traffic auto allowed     | ❌ No — must define both directions       |
| **Default Behavior**  | Deny all inbound, allow all outbound    | Allow all both ways                      |
| **Rule Evaluation**   | All rules are evaluated together        | Rules are evaluated in **number order**  |
| **Allow/Deny**        | Only **Allow** rules                    | Can **Allow and Deny**                   |
| **Use Case**          | Instance-level security (fine-grained) | Subnet-level security (broad filters)    |

---

## 🧠 Key Differences

- **Statefulness:**
  - SG automatically allows return traffic (e.g., if inbound port 443 is open, outbound response is allowed)
  - NACL is stateless: both **inbound and outbound** rules needed

- **Rule Evaluation:**
  - SG: All rules checked, first match not required
  - NACL: Rules evaluated by **rule number (lowest to highest)** → first match wins

- **Default Rules:**
  - SG has no inbound rules (deny by default)
  - Default NACL allows all traffic both ways

---

## ⚠️ Gotchas for Exam

- ❌ NACL **does not apply to individual EC2** — it applies at **subnet boundary**
- ❌ SG cannot have **deny rules**
- ✅ SG is **stateful** — exam LOVES this
- ❌ Adding NACL “allow inbound” but not outbound? Traffic will fail return path!

---

## 📌 Exam Pointers

- “Want to restrict specific IP ranges on subnet?” → ✅ NACL
- “Want EC2 to accept only HTTPS traffic?” → ✅ Security Group
- “Need to block specific IP from entering subnet?” → ✅ NACL Deny Rule
- “Traffic allowed in but failing response?” → ✅ Missing **outbound rule on NACL** or **NACL rule order issue**

---

## 🎯 Real-World Strategy

| Use Case                          | Preferred Approach     |
|-----------------------------------|-------------------------|
| Granular control per app/instance | ✅ Security Group       |
| Block IP ranges at entry          | ✅ NACL + rule ordering |
| Lock down subnet for compliance   | ✅ NACL + SG combo      |
