
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
- EFS-> Multiple ec2 can mount to it at once,IN MULTIPLE AZ
- EFS IA-> automatically pushes data to EFS IA based on lifecycle policy

![[Pasted image 20250530213443.png]]

