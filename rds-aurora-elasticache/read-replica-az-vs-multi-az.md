# scaling rds reads via read replicas

## facts

- rds read replicas needed for READ REPLICATION - increase availability & ability to recover from disaster
- 15 read replicas allowed per az
- read replicas can be persisted across three azs
- current az, cross az & cross region az
- replication is async in nature
- async meaning reads are EVENTUALLY consistent across all replicas
- just like how async works (promise and fulfulling kinda)
- each replica can be promoted to their own DB
- providing some kind of disaster recovery
- if original goes down -> another replica takes its place

## network costs of read replication

- no fees if replication happens in the same region
- yes fees if replication happens cross region

## multi-az read replica setup for disaster recovery

- can setup read replicas multi az (azA and azB)
- in this case, SYNC replication happens
- one DNS name for both source and replicas
- one DNS name provides automatic failover to replica in case of source db failure
- failure might occure due to rds instance storage failure, az disaster, loss of network..
- big advantage -> NO MANUAL INTERVENTION REQUIRED IN APPS (due to auto failover facility and one DNS name)
- THIS IS NOT USED FOR SCALING (only replication), only for INCREASING AVAILABILITY and DISASTER RECOVERY

## limitations/dont's

- can't fucking write to a read replica (why would u??)

## usecase

- have a perfect prodcution DB running supporting an app
- prod rds supports all SQL DDL (select, insert, update, delete)
- annoying BA team requests to run anaytics reports on prod rds
- you are thinking....hmmm cant let them run anayltics on my app prod rds 
- what to do what to do
- aha...read replicas
- i create read replica of my prod rds
- give them connection strings
- voila they happy, they vanish
- ++read replica only support SELECT DDLs anyways since anayltics reports only READ

## exam vvip - how to, rds single-az to multi-az?

- one click setting -> modify database
- rds will become multi az
- snapshot taken of source DB
- snapshot restored to standby DB in another az
- SYNC replication enabled between source DB in azA and snapshotted DB in azB
- ZERO DOWNTIME -> NO NEED TO STOP THE DB to configure it multi-az
