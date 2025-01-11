# rds-custom

## facts

- since rds is a fully managed db service with no access to underlying OS and EC2 instance
- standard RDS -> automated DB setup, managed autoscaling and operations
- rds custom provides all the managed goodies for DB + access to underlying OS and EC2
- means you get more control over your rds instance
- applying patches, config settings, access underlying EC2 and much more
- in short
- rds: entire DB and OS managed bt AWS
- rds-custom: full admin access to the underlying OS + EC2
- as of now, rds custom only SUPPORTED BY MS SQL SERVER & ORACLE MANAGED DB ENGINES in aws
