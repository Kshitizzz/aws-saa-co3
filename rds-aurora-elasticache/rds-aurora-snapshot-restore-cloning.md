# backups == snapshots

## rds backups

- automated backups everyday
- transaction logs backed every 5 minutes
- 1 to 35 days retiontion of backup
- set 0 days to disable automated backups
- point-in-time recovery
- snapshots are very cost effective when the usecase is 
- low usage of rds every month
- create snapshot after using in month A
- delete DB 
- in month B, restore using snapshot created in monthA
- use DB 
- take snapshot again & delete DB, rinse repeat
- GOOD TRICK TO SAVE COST IN CASE OF LOW USAGE USECASES

## aurora backups

- everything same as rds, two things
- cant disable automated backups
- have to choose b/w retiontion period of 1-35 days
- point-in-time recovery to any timestamp
- same snapshot stuff

## rds/aurora restoring

- restoring a snapshot creates new DB
- can restore both rds and aurora DBs from S3, provided backup file/snapshot image is present there
- useful when migration on-premise DBs to rds/aurora
- take backup of on-premise DB and place file in s3
- restore

## aurora cloning

- can CLONE an aurora cluster
- CLONING is faster than restoring from snapshot
- uses COPY-ON-WRITE protocol, so cloning is almost instantaneous
- COW protocol initially makes the cloned cluster point to the original storage volumes
- but as and when updates happen in the cloned DB, the updated data is copied into seperate volumes
- fucking brilliant
- very fast & cost effective
- GOOD USECASE
- creating a staging DB from a PRODUCTION DB 
- having access to PRODUCTION data without worrying about messing it up
- wow!!