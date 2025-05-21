# S3 Performance Optimization Features

## Memory Hook  
- “Big files? Break and conquer.”  
- “Far away users? Accelerate.”  
- “Want parallelism? Use range.”

---

## ✅ Multipart Uploads

### What It Is  
- Allows you to **upload large objects in parts (chunks)** concurrently.
- Supported for objects **larger than 5 MB**, **recommended for >100 MB**.
- Each part can be up to **5 GB**, total object can be **up to 5 TB**.

### Benefits  
- ✅ Faster uploads via parallel threads  
- ✅ Resume interrupted uploads (re-upload failed part only)  
- ✅ Useful for unstable networks or large backups

### How It Works  
1. Initiate multipart upload  
2. Upload each part (can be in parallel)  
3. Complete upload to combine parts into one object  

### Exam Tip  
- Multipart uploads are **not visible as objects** until the upload is completed  
- You can **abort incomplete multipart uploads** via **Lifecycle rules**  

---

## ✅ S3 Transfer Acceleration

### What It Is  
- Uses the **AWS global edge network** (CloudFront infrastructure) to **accelerate S3 uploads/downloads** over long distances.
- Works via a **dedicated CloudFront-style endpoint**: https://<bucket>.s3-accelerate.amazonaws.com

### Use Case  
- Users in **geographically distant regions**  
- Mobile apps with slow or high-latency networks  
- Centralized uploads from global clients  

### Pricing  
- 💰 More expensive than standard S3  
- Charged **per GB transferred** using the acceleration endpoint

### Exam Tip  
- Must be **explicitly enabled per bucket**  
- **Does not accelerate cross-region replication**

---

## ✅ Byte-Range Fetches

### What It Is  
- Allows applications to **download only a portion of an object** by specifying byte ranges in the GET request.
- Example:  
- Range: bytes=0–1048575


### Use Case  
- Resume **partial downloads**  
- Enable **parallelized download** of large files (e.g., video streaming, ML datasets)  
- Avoid pulling entire object into memory  

### Exam Tip  
- Often used with **multi-threaded clients**  
- Combine with **multipart upload** for both directions of performance

---

## 📌 Summary of Use Cases

| Feature               | Best For                                |
|------------------------|------------------------------------------|
| Multipart Upload       | Large object uploads (>100 MB)          |
| Transfer Acceleration  | High-latency global client uploads      |
| Byte-Range Fetch       | Efficient large object downloads, resume support |