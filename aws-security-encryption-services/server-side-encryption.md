## Server-side encryption (SSE):

- AWS service (e.g., S3) handles everything.

- S3 internally bolega: “Oye KMS, mujhe DEK de.”

- S3: DEK lo → data encrypt karo → DEK bhi encrypt karo → dono store karo.

- Tu ko kuch nahi karna hota.