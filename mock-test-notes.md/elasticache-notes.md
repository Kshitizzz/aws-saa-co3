## redis-auth

- use `Redis AUTH` to enforce users to provide a password when authenticating to execute commands on the Redis cluster
- use `transit-encryption-enabled` option to enforce enxryption during data transimission
- both above commands can be executed during the creation of redis replication / cluser: **--transit-encryption-enabled** & **--auth-token**

