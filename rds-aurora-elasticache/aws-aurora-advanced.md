# exam worthy aurora facts

## global aurora

- aurora does support cross region setup for increased disaster recovery
- but, global aurora DB is specific offering catered to cross region usecases
- 1 primary region
- but 5 SECONDARY REGIONS 
- secondary regions READ ONLY
- 16 read replicas per SECONDARY REGION
- means upto 80 read replicas, that too CROSS REGION
- fuck disaster, global aurora does not die 
- can die in case of world abomination tho (lmao?)
- MOST IMPORTANT POINT
- CROSS REPLICATION ACROSS REGION TAKES LESS THAN 1 SECOND in GLOBAL AURORA DB
- and...
- in case of primary region failover, promoting another region as primary takes less than 1 minute
- fuck me
- means RTO (return to objective [of primary region]) < 1 minute
- amazing!! 

## aurora serverless

- serverless offering 
- auto instantiation & auto scaling of DB instances based on workload
- no need to manage anything, not even storage
- everything managed

## aurora custom endpoints

- can define custome READER ENDPOINTS for specific read replicas
- usecase -> have an analytical usecase with heavy READS
- you create read replicas (read replicas can be created with different EC2 instance) for this usecase
- and define a custom READER ENDPOINT
- custom READER ENDPOINT now supports analytical stuff (voila!)

## aurora ML

- in-build integration with AWS sagemaker and AWS comprehend to support ML/NLP usecases
