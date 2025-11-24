

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


TO CREATE VOLUME:

Once copied:

- You can go to the destination Region (e.g., `us-east-1`)   
- Then create a **volume** from it there, in any AZ within that new region.

# DOUBT
### 🔹 1. **EBS snapshots are _region-specific_, not AZ-specific**

- **An EBS snapshot is stored in Amazon S3 within a specific AWS Region.**
    
- It is **not tied to a single Availability Zone (AZ)**.
    
- You can **create new EBS volumes from that snapshot in _any AZ_ within the same region.**
    

✅ Example:

> You take a snapshot of a volume in **us-east-1a**.  
> You can use that snapshot to create a new volume in **us-east-1b** or **us-east-1c** (still in `us-east-1` region).

❌ You **cannot** directly use that snapshot to create a volume in another region (like `us-west-2`) — unless you **copy** it first.

---

### 🔹 2. **Cross-Region Snapshot Copy**

If you want to use the snapshot in another region:

- Use **“Copy Snapshot”** in the AWS Console or `aws ec2 copy-snapshot` CLI command.
    
- This creates a _new_ snapshot in the destination region.
    
- Then you can create EBS volumes in _any AZ_ within that new region.
    

✅ Example:

> Copy snapshot from `us-east-1` → `eu-west-1`  
> Then create volumes in any AZ of `eu-west-1` (like `eu-west-1a`, `eu-west-1b`, etc.)

# Recycle Bin
- only EBS snapshots and AMI could be stored here
- for this we need to create retention rules -> retention period 



# snapshot pricing

- - Typically around **$0.05 per GB-month** (varies by region).
        
- **Incremental storage model**
    
    - The **first snapshot** stores a **full copy** of the volume.
        
    - Later snapshots store **only changed blocks** since the last snapshot → more cost-efficient.

### ✅ **Revision Summary (Exam-style)**

> Creating an EBS snapshot has **no upfront cost**,  
> but you’re charged for **snapshot storage in S3**, based on the **data size** (incremental).  
> Additional charges apply for **Fast Snapshot Restore** or **cross-region copies**.


| Goal                                         | Action Needed                                        | Notes                   |
| -------------------------------------------- | ---------------------------------------------------- | ----------------------- |
| Use snapshot in another **AZ** (same region) | Just **create volume** and pick a different AZ       | No need to copy         |
| Use snapshot in another **region**           | **Copy snapshot** to that region, then create volume | Needed for cross-region |