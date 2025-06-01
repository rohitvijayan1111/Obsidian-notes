
# Cloud computing

- Deployment model
	- private
	- public 
	- hybrid
- Five characteristics
	- On-demand self service
	- Broad network access:
	- Multi-tenancy and resource pooling
	- Rapid elasticity and scalability
	- Measured service
- 6 advantages:
	- Trade capital expense (CAPEX) for operational expense (OPEX)
	- Benefit from massive economies of scale
	- Stop guessing capacity
	-  Increase speed and agility 
	- Stop spending money running and maintaining data centers 
	- Go global in minutes: leverage the AWS global infrastructure
- Types of services:
	- IaaS- from os to application (virtualization is done by default)
	- Paas=from data to application is handled by us
	- Saas- everything is handled by others- we pay to use the product

- Pricing model :
	- Compute- as per usage
	- Storage- as per data stored
	- data transfer-> FREE FOR IN DATA TRAFFIC,BUT COSTS FOR SENDING DATA OUT OF AWS

# AWS Global Infrastructure 

- AWS Region ->Most of the AWS services are region based
- AWS Availability Zones
- AWS Point of Presence (POP)
	- Edge locations
	- Region cached locations ->Used to store the least frequently access to reduce the load of the edge location and the actual data center

# AWS Cloud Security
- Shared responsibility model 
	- ![[Pasted image 20250528154224.png]]
	- ![[Pasted image 20250528174947.png]]
- Root user
	- use it only for specified tasks, don't use it for daily operations , create separate account for that
- Users->represents an entity (person or an application) that interacts with AWS resources and services.
	- ⚠️ **By default**, an IAM user is created with **no permissions** — it can't access anything unless permissions are granted.
- Groups->A collection of IAM users is called an IAM group.
- policies -> IAM policies are documents. They deny or allow permissions to AWS resources and services.
	- Identifier,version,statements(Effect ->allow,deny action->on which resource principal-> applies to whom, condition,sId)
- Roles->IAM role is temporary access to services or resources.
- MFA
	- Virtual MFA, hardware key Fob, universal second factor
- How can users access AWS
	- management Console ->one time ops
	- CLI-> terminal to access resources
	- SDK-> to easily access aws resources with your application
	 > For CLI,SDK access keys are created to access those resourees
	 > Access Key ID ~= username • Secret Access Key ~= password
- Auditing tools
	- IAM Credential report (Account level)
		- Provides the status of the users under the account
	- IAM Access advisors (User level)
		-  provides the last access status of the resources allowed to be accessed by the user
		- used to modify the policy
- ![[Pasted image 20250528183407.png]]




# EC2

- 

# point to remember

- EBS -They are bound to a specific availability zone
- EBS snapshots-> incremental storage
	- EBS archive 
	- EBS recycle bin
- AMI->FOR AN REGION
- EC2 Image builder-> used to automate the creation,maintaion validate ,test ec2 ami
- EC2 instance store-> high performance,temporary storage
- EFS-> Multiple ec2 can mount to it at once,IN MULTIPLE AZ (on 100s of EC2)
- EFS IA-> automatically pushes data to EFS IA based on lifecycle policy

![[Pasted image 20250530213443.png]]


- Load Balancing
	- Vertical 
	- horizontal
	- HIgh availability -atleast 2 Az
- Scalability->abiility to accommodate a larger load by making the hardware stronger
- Elasticity ->elasticity means that there will be some “auto-scaling” so that the system can scale based on the load
- Load balancers are servers that forward internet traffic to multiple servers (EC2 Instances) downstream
- ELB is an regional construct
- Types:
	- Application: Layer 7->Static url routing ->HTTP,HTTPS,RPC
	- Network - UDP/ TCP- Layer 4 -> real time interactions,millions of request per seconds,through static ip -> TCP./UDP
	- Gateway-> acts like a firewall , all requests go to this before ec2 gets hit (Layer 3) ->GENEVE PROTOCL
	- classic -> 4 and 7 layer

ASG
- Has:
	- Minimum 
	- desired count
	- maximum count
- Types:
	- Static
	- Dynamic-> Step scaling, target scaling,
	- Scheduled scaling
	- Predictive scaling


---
Amazon S3:
- Name should be global
- But it is regional service
- Stores objects (files) in bucket(directories)
- Objects (files) have a Key • The key is the FULL path: • s3://my-bucket/my_file.txt
- here’s no concept of “directories” within buckets (although the UI will trick you to think otherwise)
- Max. Object Size is 5TB (5000GB)
- S3 Security
	- User based -> IAM policies
	- Resource based: for granular access control to specific objects/buckets
		- Object ACL
		- bucket ACL
- Bucket policy ->similar to the other policy- Grant public access,force encryption , access to another account
- Bucket settings for Block Public Access
- Amazon S3 – Static Website Hosting
	- http://buckname.s3-website-region-amazonaws.com
- Amazon S3 - Versioning
	- bucket level
	- Any file that is not versioned prior to enabling versioning will have version “null”
	 - Suspending versioning does not delete the previous versions
- Amazon S3 – Replication (CRR & SRR)
	- Must enable Versioning in source and destination buckets • Cross-Region Replication (CRR) • Same-Region Replication (SRR)


S3 Storage Classes
• Amazon S3 Standard - General Purpose
• Amazon S3 Standard-Infrequent Access (IA) 
• Amazon S3 One Zone-Infrequent Access
• Amazon S3 Glacier Instant Retrieval
• Amazon S3 Glacier Flexible Retrieval
• Amazon S3 Glacier Deep Archive 
• Amazon S3 Intelligent Tiering

Durability: • High durability (99.999999999%, 11 9’s) of objects across multiple AZ
Availability: • Measures how readily available a service is • Varies depending on storage class • Example: S3 standard has 99.99% availability = not available 53 minutes a year


• There are no retrieval charges in S3 Intelligent-Tiering
• Frequent Access tier (automatic): default tier • Infrequent Access tier (automatic): objects not accessed for 30 days • Archive Instant Access tier (automatic): objects not accessed for 90 days • Archive Access tier (optional): configurable from 90 days to 700+ days • Deep Archive Access tier (optional): config. from 180 days to 700+ days



IAM Access Analyzer for S3
• Ensures that only intended people have access to your S3 buckets • Example: publicly accessible bucket, bucket shared with other AWS account… • Evaluates S3 Bucket Policies, S3 ACLs, S3 Access Point Policies • Powered by IAM Access Analyzer


---
SNOWCONE
- AWS Snowcone is a small, rugged, and secure edge computing and data transfer device It features 2 CPUs, 4 GB of memory, and up to 14 TB of usable storage.

SNOWBALL

- • Snowball Edge Storage Optimized devices are well suited for large-scale data migrations
and recurring transfer workflows, in addition to local computing with higher capacity
needs.

Snowball Edge Compute Optimized provides powerful computing resources for use cases
such as machine learning, full motion video analysis, analytics, and local computing stacks.

SNOW MOBILE

AWS Snowmobile is an exabyte-scale data transfer service used to move large amounts of data
to AWS.
You can transfer up to 100 petabytes of data per Snowmobile, a 45-foot long ruggedized
shipping container, pulled by a semi trailer truck.


pricing

- You pay for device usage and data transfer out of AWS • Data transfer IN to Amazon S3 is $0.00 per GB
- Committed Upfront • Pay in advance for monthly, 1-year, and 3-years of usage (Edge Computing) • Up to 62% discounted pricing


---


AWS Storage Gateway
• Bridge between on-premise data and cloud data in S3
Files • Hybrid storage service to allow onpremises to seamlessly use the AWS Cloud

---

* DBMS 
	* rdbms
	* NoSQL

Benefits of DBMS managed by AWS:
	
• Benefits include: • Quick Provisioning, High Availability, Vertical and Horizontal Scaling • Automated Backup & Restore, Operations, Upgrades • Operating System Patching is handled by AWS • Monitoring, alerting

Note: many databases technologies could be run on EC2, but you must handle yourself the resiliency, backup, patching, high availability, fault tolerance, scaling…

---
RDS:
- for sql
- • It allows you to create databases in the cloud that are managed by AWS • Postgres • MySQL • MariaDB • Oracle • Microsoft SQL Server • IBM DB2 • Aurora (AWS Proprietary database)
---
Aurora:
 - Aurora is a proprietary technology from AWS
 - its cloud optimized
 - Aurora storage automatically grows in increments of 10GB, up to 128 TB 
 -  Aurora costs more than RDS (20% more) – but is more efficient
 - AURORA SERVLESS->**on-demand, auto-scaling version of Amazon Aurora**, which is a **high-performance cloud-native database** that’s compatible with **MySQL** and **PostgreSQL**.
 
 ---
 RDS Deployments: Read Replicas, Multi-AZ
- Can create up to 15 Read Replicas • Data is only written to the main DB

- Multi-AZ: • Failover in case of AZ outage (high availability) • Data is only read/written to the main database • Can only have 1 other AZ as failover
---
Amazon ElastiCache Overview
• The same way RDS is to get managed Relational Databases… • ElastiCache is to get managed Redis or Memcached • Caches are in-memory databases with high performance, low latency • Helps reduce load off databases for read intensive workloads

---
DynamoDB
• Fully Managed Highly available **with replication across 3 AZ** • NoSQL database - not a relational database • Scales to massive workloads, distributed “serverless” database • Millions of requests per seconds, trillions of row, 100s of TB of storage
- Standard & Infrequent Access (IA) Table Class

DynamoDB Accelerator - DAX
• Fully Managed in-memory cache for DynamoDB

Difference with ElastiCache at the CCP level: DAX is only used for and is integrated with DynamoDB, while ElastiCache can be used for other databases

DynamoDB – Global Tables
• Make a DynamoDB table accessible with low latency in multiple-regions • Active-Active replication (read/write to any AWS Region)

---

 Redshift Overview
• Redshift is based on PostgreSQL, but it’s not used for OLTP • It’s OLAP – online analytical processing (analytics and data warehousing) • Load data once every hour, not every second

Columnar storage of data (instead of row based) • Massively Parallel Query Execution (MPP), highly available

---

Amazon EMR
• EMR stands for “Elastic MapReduce” • EMR helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data


Auto-scaling and integrated with Spot instances • Use cases: data processing, machine learning, web indexing, big data…

---

Amazon Athena
• Serverless query service to analyze data stored in Amazon S3

---
Amazon QuickSight
• Serverless machine learning-powered business intelligence service to create interactive dashboards

---
DocumentDB
• Aurora is an “AWS-implementation” of PostgreSQL / MySQL … • DocumentDB is the same for MongoDB (which is a NoSQL database)
• MongoDB is used to store, query, and index JSON data • Similar “deployment concepts” as Aurora • Fully Managed, highly available with replication across 3 AZ • DocumentDB storage automatically grows in increments of 10GB

---
Amazon Neptune
• Fully managed graph database • A popular graph dataset would be a social network • Users have friends • Posts have comments • Comments have likes from users • Users share and like posts…
• Highly available across 3 AZ, with up to 15 read replicas

---
Amazon Timestream
• Fully managed, fast, scalable, serverless time series database
• Automatically scales up/down to adjust capacity

---
Amazon QLDB
• QLDB stands for ”Quantum Ledger Database” • A ledger is a book recording financial transactions • Fully Managed, Serverless, High available, Replication across 3 AZ • Used to review history of all the changes made to your application data over time • Immutable system: no entry can be removed or modified, cryptographically verifiable

---
Amazon Managed Blockchain
• Blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority.
• Amazon Managed Blockchain is a managed service to: • Join public blockchain networks • Or create your own scalable private network

---
AWS Glue
• Managed extract, transform, and load (ETL) service • Useful to prepare and transform data for analytics • Fully serverless service

---
	DMS – Database Migration Service Source DB
• Quickly and securely migrate databases to AWS, resilient, self healing
• The source database remains available during the migration
EC2 instance Running DMS
• Supports: • Homogeneous migrations: ex Oracle to Oracle
Target DB
• Heterogeneous migrations: ex Microsoft SQL Server to Aurora

---




