

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
- EBS Snapshot Archive-> used to archive, it to reduce cost, could take upto 24 to 72 hrs
- Recyle Bin for archive-> used to prevent accidental deletion, retention duration could be from 1 day to 1year
## Fast Snapshot Restore (FSR)** — AWS EBS

### 🧩 **What it is:**

**Fast Snapshot Restore (FSR)** ensures that **EBS volumes created from a snapshot** are **fully initialized and instantly performant** from the moment they’re created.

Normally, when you restore an EBS volume from a snapshot:

- The data is **lazy-loaded** (fetched on first access from Amazon S3).
    
- This means the **first reads are slow** — because AWS is pulling data blocks from S3 in the background.
    

With **Fast Snapshot Restore**, that delay disappears.

> 💡 FSR = No more initial slow reads — volume performs at full speed immediately after creation.

---

### ⚙️ **How it works:**

- You **enable FSR** on a specific snapshot **per Availability Zone (AZ)**.
    
- AWS **pre-warms** that snapshot in the background.
    
- When you create a new EBS volume from that snapshot **in the same AZ**, it’s **instantly ready** for full-performance I/O.
    

---

### 💰 **Billing:**

- You **pay hourly** for each snapshot with FSR **enabled** per AZ.
    
- Example: Enabling FSR for one snapshot in two AZs = 2 FSR charges.
    
- You’re billed until you disable it.


> NOTE
> You can’t attach a snapshot directly to an EC2 instance —  
	it must first be **restored as an EBS volume**, then attached.


✅ **Exam-Ready Summary (2 lines):**

> Stopping an EC2 instance does **not delete** data — the EBS volume stays attached.  
> “Delete on Termination” only deletes the volume **when the instance is terminated**, not stopped.

### ✅ **Revision Summary**

> When you **stop** an EC2 instance, you stop paying for **compute**,  
> but still pay for **EBS storage** (and provisioned IOPS, snapshots, or Elastic IPs if allocated).


# TO COPY EBS SNAPSHOT TO ANOTHER REGION:

#### Steps:

1. Go to **EC2 → Snapshots**
2. Select your snapshot
3. Click **Actions → Copy snapshot**
4. Choose the **destination Region** (e.g., from `eu-north-1` → `us-east-1`)
5. Click **Copy Snapshot**


TO CREATE 