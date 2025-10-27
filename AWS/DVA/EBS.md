

# EBS
- is a network drive you can attach to your instances while they run
- It allows your instances to persist data, even after their termination
- They are bound to a specific availability zone
- They can only be mounted to one instance at a time (at the CCP level)
- provisioned capacity (size in GBs, and IOPS) 
	-  You get billed for all the provisioned capacity
- Controls the EBS behaviour when an EC2 instance terminates
	-  By default, the root EBS volume is deleted (attribute enabled) 
	- By default, any other attached EBS volume is not deleted (attribute disabled

# How to create EBS:
- go to EBS, create volume
- choose the volume type , size, the az that u need this in
- so in the EBS listing dashboard, click on the EBS volume and in actions choose, attach to instance, to attach this to an EC2
- For the EBS's root volume attached to an EC2, for it delete on termination is enabled by default.


# EBS Snapshot

- It is used to create a backup copy of a EBS volume at a point
- it is recommended to detach it from instance before taking a snapshot
- using EBS snapshot, we can import the EBS to another AZ/ Region


## Features:
- EBS Snapshot Arch