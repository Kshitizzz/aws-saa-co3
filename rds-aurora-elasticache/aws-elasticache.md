# elasticache - redis or memcached

## facts

- managed cached service just like rds
- two engines or cache tech: redis or memcached
- everything managed by aws
- cache is in-memory database to store frequently accessed things
- multi-az for HA, read-replicas & automatic failover supported

## why cache?

- use cache to reduce stress on main db for read heavy workloads
- by reducing the number of trips to DB for reading a frequently read data
- also helps in making application stateless
- managing sessions to determine if user has logged in recently
- store user log in state in cache so user dont have to login again [ofcourse thier is timeout]

## quirks

- have to setup a cache invalidation strategy
- cache invalidation: refresh data stored in cache so that its not stale
- also using elasticache means making code changes to yoyr application
- not plug and play, need to manually query and invalidate cache

## redis vs memcached

### redis

- multi-az setup supported
- highly available as read-replicas can be setup multi-az
- backup and restore feature available

### memcached

- no multi-az setup, hence not highly-available
- but, supports sharding, hence multi-node setup
- data is partitioned across multiple nodes, so better performance
- also, multi-threaded
- non-persistent

## cache usage patterns

- (1) lazy loading: data only read from DB in case of a cache miss
- two terms: cache hit  and cache miss
- cache hit means data is available in cache and cache miss otherwise
- in case of cache miss, update cache: read from DB & write to cache
- (2) write through: add/update cache each time data is written to db
- (3) session management: manage user sessions accross multiple instance of application to determine if user login is still valid
- store temp session data in cache basically

## redis auth methods

- security groups (1st layer)
- redis auth token & user/pw based auth (2nd layer)
- IAM auth supported for redis
- IAM policies can be only used for AWS API level security
- who can access what through AWS API

## encryption

- redis supports in-flight SSL encryption
- memcached supports more advanced SASL based encryption

# very popular redis usecase

- redis is used in gaming leaderboards tech
- gaming leaderboards are complex and real-time
- redis used sorted sets to enable ranking on gaming leaderboards
- each time an element is entered, its sorted and ranked in real time
- redis sorted sets guarantee both uniqueness and correct order