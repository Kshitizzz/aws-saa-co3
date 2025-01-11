# aurora - pinnacle of distributed data storage or proprietary bullshit????

## facts

- aws aurora proprietary tech by AWS, closed source
- like RDS but two engines supported as of now - mysql and postgresql
- connection to aurora pretty simple, just like connection with mysql or postgresql (ODBC)
- 20% expensive than RDS, but it more efficient
- its HA native, supports HA out of the box
- storage is also autoscaling by a factor of 10GB
- storage starts from 10 GB upto 128 TB
- auto failover is instantaneous
- restore data to any point in time WITHOUT USING BACKUPS 

## aurora instance architecture

- has ONE master instance
- ALL WRITES HAPPEN TO MASTER INSTANCE only
- upto 15 read replicas supported across 3 AZs (just like RDS)
- read-replicas support AUTO SCALING (upto 15)
- aurora supportrs connection loadbalancing during reads via READER ENDPOINT
- clients connect to READER ENDPOINT for all read requests
- similarly, write happens via WRITER ENDPOINT (to support autofailover)
- WRITER ENDPOINT always points to the MASTER
- client send write requests to WRITER ENDPOINT (no load balancing needed since write requests go to master only)
- cross region replication supported (like RDS)
- AUTOMATED FAILOVER FOR MASTER IN LESS THAN 30 SECONDS

## aurora storage and data replication (copies)

- storage 10 GB - 128 TB
- storage striped/distributed across 1000s of volumes
- aurora is super cloud native 
- at a given point in time, 6 COPIES ARE PERSISTED ACROSS 3 AZs for a given block of data
- 4 COPIES ARE NEEDED FOR WRITE (why??)
- 3 COPIES ARE NEEDED FOR READS (why??)
- storage is shared across MASTER and READ REPLICA instances
- ah yes, wizard shit - self healing via peer-to-peer replication also there
- 1 out of 6 copies of data gets corrupted, but is magically recovered via self healing
- WOW!

