# DynamoDB
[Java with Localstack DynamoDB](https://medium.com/dandelion-tutorials/using-dynamodb-localstack-with-spring-boot-and-spring-data-b7f487bd9e9d) 

# AWS re:Invent 2022

## [DynamoDB](https://www.youtube.com/watch?v=SC-YAPgJpms&t=1475s) 
### Data Modeling Process
- Create ER diagram
- List your access patterns

| Write Pattern | Item(s) altered | Condition(s) | Frequency | Notes |
|---|---|---|---|---|

- Design your primary keys to handle your access patterns
### Single Item actions
- Must include partion key (or partion key + sort key)
- ULIDs (Unique, time-sortable IDs)
### Related Data - Embedded vs Item Collection
- Embedded When:
	- Small, bounded set of relations
	- Not searching by the relations directly
- Item collection + query when:
- Large, unbound set of relations
- want to fetch the related item directly
### Secondary Indexes
- Data from your table gets copied onto separate partitions with a new primary key
	- Primary key becomes sort key
	- Not a true primary key - no uniqueness
- Allows for read-based operations
	- No writes
- Can provide filtering
- Sparse index
### Single Table Design
- Putting multiple, heterogenous entities into a single table
- Using generic primary key names

| Primary Key | Sort Key | Type |
| --- | --- | --- |
| USER#dude | 12355 | Quest
| | USER#dude | User

- Can improve performance by reducing requests
	- Prejoining data at write time instead of read time
- Can reduce costs
- Lower maintenance burden
- It forces you to think about DynamoDB correctly
	- Think about access patterns first, not data normalization
- [Java - Single Table Design Blog Post](https://aws.amazon.com/blogs/database/amazon-dynamodb-single-table-design-using-dynamodbmapper-and-spring-boot/) 
### Transactions
- `TransactWriteItem()`
- Similar to Relational DBs
	- 2-phase commits
	- ACID semantics
	- Serializable isolation between transactions and other writes

## [Outpost](https://youtu.be/OUNJ0F73HSs)
### Edge Computing
- Used for the following requirements
	- Low latency
	- Local data processing
	- Data residency
	- Migration and Modernization
- Location Ranges
	- Regions -> Metro Areas -> On Prem -> Remote & Limted Connectivity Locations -> IoT
### Rack vs Server
- Rack
	- Industry-Standard 42U rack
	- 80in tall
	- Fully assembled and installed by AWS
- Servers
	- 1U Form Factor & 2U Form Factor
		- 1.75 - 3.5in tall
	- Rack mountable
	- AWS can install for you or self install
### Services
- Ran locally
	- Elastic Cloud Compute
	- EBS
	- EBS Local snapshots
	- S3
	- ECS
	- EKS
	- Relational Database Service
	- EMR
	- ElastiCache
	- CloudEndure
	- Load Balancer
	- VMware
- No DynamoDB Locally
	- ScyllaDB same API as DynamoDB
		- [ScyllaDB on AWS outpost](https://www.scylladb.com/2020/09/15/scylla-cloud-on-aws-outposts/) 
### System
- Runs on the AWS Nitro System
	- Nitro cards
	- Nitro Security chip
	- Nitro Hypervisor
