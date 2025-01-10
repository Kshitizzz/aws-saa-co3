# aws rds

## facts 

	- managed database service by AWS
	- extra service + aws autoscalability options (vertical + horizontal)
	- timely backups
	- allows Point in Time Restore: restore to specific timestamps
	- read replicas for improved read performance
	- disaster recovery - multi az setup
	- OS patching 
	
## limitations

	- cant SSH into your instances (which you can do actually if you'd host your own DB instance on EC2)

## exam layak features

	- storage auto scaling
	- when rds detects free space ille -> it auto scales storage dynamically
	- need to set Maximum Storage Threshold
	- number to determine the max storage allowed for auto scaling
	- RDS auto scales storage on three conditions
		○ free storage less than 10% of allocated storage
		○ low-storage lasts at least 5 mins
		○ 6 hours have passed since last modification (to scale down ??)
	- aws rds supports all storage engines (mysql, postgresql, sql server, ibm db2, mariadb, aurora db (aws proprietery))
	- rds read replicas for read scalability 
	- to scale read operations on rds
	- upto 15 read replicas allowed
	- across 3 Azs
		○ within AZ
		○ cross AZ
		○ cross region
	- like mumbai az fata, its okay -> check if noida az working -> noida az bhi fata, its okay -> check if europe region az working -> wo bhi fata -> chud gye guru!
	
 ## major usecase 
	- apps with UNPREDICTABLE WORKLOADS
	- to scale up and down as per need of the app
	
