	1. Global flat storage service
	2. Resilient on a REGIONAL level -- if one region fails, it doesn’t even matter -- data is replicated across multiple regions
	3. Can store everything -- unstructured data
	4. DEFAULT STORAGE SERVICE IN AWS
	5. S3 components:
		a. Objects
			i. Key-value pairs
			ii. Value size can range from 0 BYTES to 5 TB
		b. Buckets
			i. Bucket name should be GLOBALLY UNIQUE, not regional, account unique -- IMP
			ii. Can hold unlimited number of objects -- infinite scalable storage system -- unlimited storage
			iii. FLAT storage -- no file structure -- conceptual folders can be created by using / in object name
			iv. Eg -- study_material/videos/video-1.mp4
	6. EXAM POWER UPS
		a. Bucket names are globally unique
		b. Bucket name should be 3-63 chars long, all lowercase and no underscores
		c. Starts with a lowercase letter or a number
		d. 100 SOFT LIMIT and 1000 HARD LIMIT on # of buckets per ACCOUNT -- IMP
		e. S3 >> Object Storage system --  NOT FILE/BLOCK STORAGE SYSTEM
		f. Cant MOUNT an S3 Bucket as in C Drive in windows
![image](https://github.com/user-attachments/assets/b1752587-906e-4859-ab3b-6a165632ed92)
