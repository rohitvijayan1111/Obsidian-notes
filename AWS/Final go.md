
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






**DOCKER**

- • Docker is a software development platform to deploy apps • Apps are packaged in containers that can be run on any OS • Apps run the same, regardless of where they’re run
- Where Docker images are stored?
	- Public: Docker Hub
	- Private: Amazon ECR (Elastic Container Registry)



**ECS-Elastic Container service**
- Launch Docker containers on AWS
- **You must provision & maintain the infrastructure (the EC2 instances)**
- AWS takes care of starting / stopping containers
- Has integrations with the Application Load Balancer

ECS can be container can be managed in two ways:
- EC2 instances 
- serverless- fargate


Fargate
• Launch Docker containers on AWS
• You do not provision the infrastructure (no EC2 instances to manage) – simpler!
• Serverless offering • AWS just runs containers for you based on the CPU / RAM you need


ECR
• Elastic Container Registry • Private Docker Registry on AWS
• This is where you store your Docker images so they can be run by ECS or Fargate


Amazon EKS
• EKS = Elastic Kubernetes Service • Allows you to launch managed Kubernetes clusters on AWS
• Kubernetes is an open-source system for management, deployment, and scaling of containerized apps (Docker)
• Containers can be hosted on: • EC2 instances • Fargate (Serverless)
• Kubernetes is cloud-agnostic (can be used in any cloud – Azure, GCP…)

## 🚀 What is **AWS Lambda**?

**AWS Lambda** is a **serverless compute service** that lets you **run code without provisioning or managing servers**. You simply upload your code, and Lambda runs it **in response to events** — automatically handling the **scaling, availability, and infrastructure** behind the scenes.

> ✅ **Key Idea**: You write code, AWS runs it **on demand** in a fully managed environment.

## 📦 Key Characteristics

|Feature|Description|
|---|---|
|**Serverless**|No servers to manage — AWS takes care of provisioning and scaling|
|**Event-driven**|Code runs in response to triggers like HTTP requests, file uploads, or database changes|
|**Auto-scaling**|Scales instantly from 0 to thousands of requests in parallel|
|**Short-lived**|Each execution is stateless and limited to **15 minutes max**|
|**Languages supported**|Node.js, Python, Java, Go, .NET, Ruby, and custom runtimes|
|**Pay only for what you use**|You pay **per request** and **duration (per ms)** of execution|



----

• You can find overall pricing information here: https://aws.amazon.com/lambda/pricing/
• Pay per calls: • First 1,000,000 requests are free • $0.20 per 1 million requests thereafter ($0.0000002 per request)
• Pay per duration: (in increment of 1 ms) • 400,000 GB-seconds of compute time per month for FREE • == 400,000 seconds if function is 1GB RAM • == 3,200,000 seconds if function is 128 MB RAM • After that $1.00 for 600,000 GB-seconds
• It is usually very cheap to run AWS Lambda so it’s very popular


**Lambda Billing: • By the time run x by the RAM provisioned • By the number of invocations**

---
## 🌐 What is Amazon API Gateway?

**Amazon API Gateway** is a **fully managed service** that enables you to **create, publish, maintain, monitor, and secure APIs** at any scale. It acts as a **"front door"** for your applications to access **backend services** such as:

- AWS Lambda functions
    
- HTTP endpoints
    
- AWS services (via AWS integration)
    
- Other AWS resources
    

> 📌 API Gateway allows you to expose RESTful, HTTP, and WebSocket APIs securely and efficiently.

---

AWS Batch

- used to run batch processing
- it automates manages infra and provisions it
- it uses AWS ECS and docker for submit the job
- we need to just submit the job and AWS Batch handles the rest

---
Amazon Lightsail
• Virtual servers, storage, databases, and networking • Low & predictable pricing • Simpler alternative to using EC2, RDS, ELB, EBS, Route 53… • Great for people with little cloud experience!

Has high availability but no auto-scaling, limited AWS integrations

---
---
**AWS CloudFormation**

**AWS CloudFormation** is a tool from Amazon Web Services (AWS) that helps you **set up and manage your cloud resources automatically**, like servers, databases, networks, and more — **using code instead of clicking around in a web dashboard**.

### 🌐 What is **Infrastructure Composer**?

**Infrastructure Composer** is a **visual tool in AWS** that helps you **build CloudFormation templates without writing code manually**. It lets you **drag and drop AWS resources** (like EC2 instances, S3 buckets, etc.) on a canvas and then **generates the CloudFormation code for you**.

---

**WS Cloud Development Kit (CDK)**
• Define your cloud infrastructure using a familiar language: • JavaScript/TypeScript, Python, Java, and .NET
• The code is “compiled” into a CloudFormation template (JSON/YAML)
• You can therefore deploy infrastructure and application runtime code together

---
### 🌱 What is **AWS Elastic Beanstalk**?

**Elastic Beanstalk** is a **Platform-as-a-Service (PaaS)** offering from AWS. It lets you **deploy and manage web applications quickly** — without needing to manually configure the underlying infrastructure like servers, databases, networking, etc.

---
### 🚀 What is **AWS CodeDeploy**?

**AWS CodeDeploy** is a **deployment service** that helps you **automate the process of updating code** on:

- EC2 instances
    
- On-premise servers
    
- Lambda functions
    
- ECS services
    

It doesn’t build your app or define infrastructure — instead, it **manages how new versions of your code get installed and activated** on your servers or services.

---
### 🧾 What is **AWS CodeCommit**?

**AWS CodeCommit** is a **fully managed Git-based source control service** — basically, it’s AWS’s version of GitHub or GitLab, but hosted inside AWS.

You can:

- Push and pull code like any other Git repo
    
- Store private repositories
    
- Integrate with AWS services (CodeBuild, CodeDeploy, etc.)
    
- Use IAM for access control

---

### 🚀 What is **AWS CodeBuild**?

**AWS CodeBuild** is a **fully managed build service** that compiles your source code, runs tests, and produces deployable artifacts (like application packages or Docker images).

Basically, it automates the **“build”** step in your Continuous Integration (CI) or Continuous Delivery (CD) pipeline.

---
AWS CodePipeline
• Orchestrate the different steps to have the code automatically pushed to production • Code => Build => Test => Provision => Deploy • Basis for CICD (Continuous Integration & Continuous Delivery)

---
AWS CodeArtifact
• Software packages depend on each other to be built (also called code dependencies), and new ones are created
• Storing and retrieving these dependencies is called artifact management

Developers and CodeBuild can then retrieve dependencies straight from CodeArtifact

---

### 🚀 What is **AWS Systems Manager (SSM)**?

AWS Systems Manager is a **centralized management service** that helps you **view, control, and automate operational tasks** across your AWS resources — like EC2 instances, on-prem servers, and more — all from one place.

How Systems Manager works
• We need to install the SSM agent onto the systems we control

### 🔐 What is **SSM Session Manager**?

It’s a **secure, auditable, and easy way to access your EC2 instances (or on-premises servers)** without needing traditional SSH.

---

### Why it’s awesome:

- **No need to open port 22** (SSH) on your instances → reduces attack surface
    
- **No SSH keys or bastion hosts** → simplifies access management
    
- Supports **Linux, macOS, and Windows** servers
    
- Sessions and commands can be **logged to S3 or CloudWatch Logs** for audit and compliance
    

---

### How to **start a session and execute commands**:

1. **Prerequisites:**
    
    - EC2 instance must have the **SSM Agent installed and running** (most modern AMIs have it preinstalled)
        
    - The instance role must have **IAM permissions** allowing SSM access (e.g., `AmazonSSMManagedInstanceCore` policy)
        
    - Instance needs outbound internet or VPC endpoint to SSM
        
2. **Start a session:**
    

- Using AWS Console:
    
    - Go to Systems Manager > Session Manager
        
    - Select your instance and click **Start session**

---

Systems Manager Parameter Store
Applications plaintext
• Secure storage for configuration and secrets • API Keys, passwords, configurations… • Serverless, scalable, durable, easy SDK • Control access permissions using IAM • Version tracking & encryption (optional

---
---

## 🌐 What is Amazon CloudFront?

**Amazon CloudFront** is a **Content Delivery Network (CDN)** service from AWS that delivers data, videos, applications, and APIs to users globally with **low latency** and **high transfer speeds**.

> It speeds up distribution of your content by caching copies at **edge locations** close to your users worldwide.

---

## How CloudFront Works

1. You configure CloudFront to deliver content from an **origin** — typically an S3 bucket, an HTTP server (like your web server), or an AWS Elastic Load Balancer.
    
2. When a user requests content (e.g., a website image), the request is routed to the **nearest CloudFront edge location**.
    
3. If the content is already cached at the edge location, CloudFront delivers it immediately.
    
4. If not cached, CloudFront fetches it from the origin, caches it, then delivers it to the user.
    
5. Subsequent users near that location get the cached content quickly without going all the way to the origin.

---
CloudFront vs S3 Cross Region Replication

cloudFront
- Great for static content that must be available everywhere

S3 Cross Region Replication
- Great for dynamic content that needs to be available at low-latency in few regions

---
S3 Transfer Acceleration
• Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target reg


---

AWS Global Accelerator

**AWS Global Accelerator** is a **networking service** that improves the **availability and performance** of your internet-facing applications by directing user traffic through the **AWS global network infrastructure**.

---

### 🔍 **What It Does**

- **Provides 2 static Anycast IP addresses** to act as a **global entry point** for your application.



### 🌐 **AWS Wavelength – Explained Simply**

**AWS Wavelength** brings **AWS cloud services** closer to **mobile users and devices** by deploying AWS infrastructure **at the edge of telecom providers' 5G networks**.


### 🏙️ **AWS Local Zones – Explained Clearly**

**AWS Local Zones** are a type of **AWS infrastructure deployment** that brings **compute, storage, and select AWS services closer to large population centers**, **outside of the main AWS Regions**.





----
---
---
---


Amazon SQS – Standard Queue

- Fully managed service (~serverless), use to decouple applications
- Scales from 1 message per second to 10,000s per second
- • Default retention of messages: 4 days, maximum of 14 days 
	- • No limit to how many messages can be in the queue


### 📊 **Amazon Kinesis Data Streams (KDS) – Deep Dive**

**Amazon Kinesis Data Streams** is a **real-time data streaming service** that allows you to **collect, process, and analyze streaming data at massive scale**.

Amazon SNS
• The “event publishers” only sends message to one SNS topic • As many “event subscribers” as we want to listen to the SNS topic notifications • Each subscriber to the topic will get all the messages


---

### 📬 **Amazon MQ – Detailed Explanation**

**Amazon MQ** is a **managed message broker service** for **Apache ActiveMQ** and **RabbitMQ**. It enables applications to communicate with each other using **message queues**, while **offloading the complexity** of setting up and maintaining the underlying broker infrastructure.


---
### 📊 Amazon CloudWatch Metrics – Explained in Detail ->Monitor, log and alert

**Amazon CloudWatch Metrics** are **time-ordered data points** that represent the performance of your AWS resources or applications. They are a **core part of CloudWatch**, which is AWS’s native monitoring and observability service.

- • You need to run a CloudWatch agent on EC2 to push the log files you want even for on premis

---
# Event Bridge

**Amazon EventBridge** is a **serverless event bus** service that helps different applications (AWS services, SaaS apps, or your own apps) communicate with each other using **events** in **real time**.


----


### **AWS CloudTrail – Explained in Detail**

**AWS CloudTrail** is a **logging and auditing service** that **records all actions** taken within your AWS account. It helps you understand **who did what**, **when**, and **from where** — making it critical for **security, compliance, and troubleshooting**.

---
