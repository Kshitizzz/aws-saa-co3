# proxy (i finally understood the meaning of the word proxy)

## note - proxy is applicable for both rds and aurora 

- rds proxy pools and shares open DB connections with the client apps
- so, client apps dont need to manage DB connections themselves
- always a mess this stuff
- some conn left open leading to fucked up db performance
- now prox is fully managed by aws
- proxy reduces load on DB since connections are limited and greatly managed leading to overall efficiency gains in-terms of dB compute and RAM
- proxy enforces IAM auth to client apps, so no user/pw login and hence more secure
- third, proxy can only be accessed via a private VPC, more isolated hence secure
- also, reduces rds/aurora failover time by 66%
- since proxy handles the failover by pointing to the replica promoted to be the main DB
- BEST FUCKING USECASE
- lambda functions
- this little buggers can sprout up multiple instances of themselves to support compute (right?)
- and if each one were to open a conn with DB, then its a messy situation leading to high stress on DB
- timeouts etc...
- but, proxy efficiently manages and pools connections
- so lambdas connect to the rds proxy and go on with their biz
- proxy is like the hot assistant outside the CEOs office
- but with actual skills (lmao?)
