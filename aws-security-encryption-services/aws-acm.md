# AWS Certificate Manager (ACM)

## Memory Hook

- "SSL is good. Managed SSL is better. Automated renewals = headache-free HTTPS."
- Or
- “Let AWS babysit your certificates.”

## Must-Know Core Concepts

- AWS Certificate Manager (ACM) lets you **provision, manage, and deploy SSL/TLS certificates** for use with AWS services.
- It **automates renewal** of certificates and **does not require manual rotation**.
- Two types of certificates:
  - **Public certificates**: Issued by ACM for use with domain names you own (free of cost).
  - **Private certificates**: Issued using AWS Private CA (paid service), often used internally within organizations.
- ACM certificates can be used with:
  - **Elastic Load Balancers (ALB, NLB)**
  - **CloudFront**
  - **API Gateway**
  - **AWS Global Accelerator**

## Nuances & Edge Cases

- ACM certificates are **regional**, except when used with **CloudFront**, which is a **global service** — so the cert must be in **us-east-1**.
- **ACM does not support export** of public certificates — you cannot use the cert outside AWS infra unless it's a private cert via AWS Private CA.
- **Private CA** allows internal usage and fine-grained control but is **chargeable**.
- ACM **validates domain ownership** via:
  - DNS validation (preferred)
  - Email validation (deprecated slowly)
- You **cannot attach** ACM certificates to EC2 directly — use with ELB or CloudFront.

## Exam Pointers

- You’ll get questions asking **which service allows automatic TLS certificate management** — answer is **ACM**.
- If you see a scenario needing secure HTTPS endpoints **without worrying about renewals**, go with **ACM**.
- For **CloudFront + HTTPS**, make sure the cert is in **us-east-1** (global distribution region).
- For **private internal communication**, choose **AWS Private CA** with ACM.
