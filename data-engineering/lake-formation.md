# AWS Lake Formation – Centralized Permissions & Data Lake Security

## Memory Hook  
- “Lake Formation = IAM for data lakes”  
- “Build once, secure everywhere — column, row, table”

---

## ✅ What Is AWS Lake Formation?

> A managed service to build, secure, and manage **data lakes on AWS**  
> Built **on top of AWS Glue**, Lake Formation adds:
- Centralized access control
- Fine-grained data permissions
- Data lake ingestion and cataloging
- Integration with **Athena, Redshift Spectrum, EMR, SageMaker**

---

## 🧩 Lake Formation Key Components

| Component               | Description                                                  |
|--------------------------|--------------------------------------------------------------|
| **Data Lake Admin**      | Superuser who can delegate permissions                      |
| **Permissions**          | Column-level, table-level, database-level controls          |
| **LF Tag-Based Access**  | Dynamic access control using metadata tags                  |
| **Resource Sharing**     | Secure sharing across accounts (via **Resource Links**)     |
| **Row/Column Filters**   | ✅ Row-level security + column masking                       |
| **Data Catalog**         | Uses Glue Catalog under the hood                            |

---

## 🔐 Lake Formation Centralized Permissions

> Unlike Glue (which uses IAM), Lake Formation uses its own **grant-based permission model** to control data access.

| Feature                    | IAM/Glue Catalog ACL               | Lake Formation Permissions                |
|----------------------------|------------------------------------|--------------------------------------------|
| Auth Model                 | IAM policies only                  | ✅ Lake Formation Grants + IAM             |
| Column-level control       | ❌ No                              | ✅ Yes                                      |
| Row-level security         | ❌ No                              | ✅ Yes (via filters)                        |
| Centralized access         | ❌ Scattered (per service)         | ✅ One place: Lake Formation console        |
| Cross-account sharing      | ❌ Hard via Glue-only              | ✅ Easy via **Resource Links**             |

---

## 🧠 LF Permissions Object Model

| Scope     | Permissions You Can Grant                                     |
|-----------|---------------------------------------------------------------|
| **Database** | `CREATE_TABLE`, `ALTER`, `DROP`, `DESCRIBE`, `GRANT`         |
| **Table**    | `SELECT`, `INSERT`, `DELETE`, `ALTER`, `DESCRIBE`, `GRANT`   |
| **Column**   | ✅ Column-level `SELECT`                                       |
| **LF Tags**  | `ASSOCIATE`, `DESCRIBE`, `GRANT_WITH_LF_TAG_EXPRESSION`       |

🧠 Permissions are granted to **IAM principals** (users, roles)

---

## ✅ Cross-Account Access via Resource Links

1. **Producer account** shares a DB/Table
2. **Consumer account** creates a **resource link**
3. Consumer uses Athena/Redshift Spectrum/EMR to query via that link

✅ Granular control: producer can revoke access any time  
✅ All permissions are still enforced centrally by Lake Formation

---

## ✅ Lake Formation Tag-Based Access Control (LF-TBAC)

> Grant access based on **LF Tags** (key-value labels)

### Example:
- Table `transactions` has LF tag: `Env=Prod`
- Analyst role has policy: `SELECT where Env=Prod`

🧠 Enables:
- Dynamic access management
- Attribute-based access control (ABAC)
- Multi-tenant isolation

---

## 🔄 IAM vs Lake Formation Permissions – How They Work Together

| Layer         | Purpose                              |
|----------------|----------------------------------------|
| **IAM**         | Authenticate user + allow service call (e.g., Athena:StartQueryExecution) |
| **Lake Formation** | Authorize access to the underlying **data objects**       |

🧠 IAM = **can run the tool**  
🧠 LF = **can access the actual data**

---

## 🧠 Row-Level Security (Filter Expressions)

- Define filter policy per principal:
```sql
customer_id = '${userid}'

Dynamically restrict access at query time

Works in Athena, Redshift Spectrum, and EMR

✅ Real-World Use Cases
Use Case	Lake Formation Feature Used
Analyst in account A queries data in account B	✅ Resource Links + Cross-Account Sharing
Limit access to only sensitive columns	✅ Column-level SELECT permission
Secure data per tenant in multi-tenant app	✅ Row-level filters (tenant_id = ${user})
Dynamic permissioning across dozens of datasets	✅ LF Tag-Based Access Control (LF-TBAC)

📌 Exam Pointers
“Grant read access to only specific columns in a table?” → ✅ Use Lake Formation permissions

“Allow Redshift Spectrum to access S3 table securely?” → ✅ Catalog in Glue + Permissions in LF

“User has IAM permissions but access denied in Athena?” → ✅ Lake Formation permission missing

“Secure data sharing across accounts in Athena?” → ✅ Resource Links in Lake Formation

“Control data access dynamically by tags?” → ✅ LF-TBAC

“Allow read only rows with specific conditions?” → ✅ Row-level security filter

vbnet
Copy
Edit
