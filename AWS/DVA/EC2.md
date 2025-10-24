

# Creating EC2 Instance

## **Steps to Create an EC2 Instance**

### 1️⃣ **Name and Tags**

- Give your instance a **name tag** (for easy identification).
    
- Tags are key–value pairs used for organizing and managing resources.
    

---

### 2️⃣ **Choose an AMI (Amazon Machine Image)**

- AMI defines the **OS + preinstalled software + configuration**.
    
- Types:
    
    - Amazon Linux 2, Ubuntu, Windows, etc.
        
    - You can also use **custom AMIs** you create.
        
- Essentially: AMI = _template for your EC2 instance._
    

---

### 3️⃣ **Choose Instance Type**

- Defines the **hardware configuration** — CPU, memory, storage, and networking.
    
- Example:
    
    - `t2.micro` → Free-tier eligible (1 vCPU, 1 GB RAM)
        
    - `m5.large`, `c5.xlarge` → higher compute/memory.
        

---

### 4️⃣ **Create / Choose a Key Pair**

- Used to securely connect (SSH for Linux, RDP for Windows).
    
- You download a `.pem` or `.ppk` file when created — **keep it safe**.
    
- Without it, you can’t access the instance via SSH later.
    

---

### 5️⃣ **Configure Network Settings**

- Choose:
    
    - **VPC** (Virtual Private Cloud)
        
    - **Subnet** (Availability Zone)
        
    - **Auto-assign Public IP** (for internet access)
        
- **Security Group** = virtual firewall
    
    - Controls **inbound/outbound** traffic
        
    - Default name if not customized: `launch-wizard-1`
        
    - Common inbound rules:
        
        - `SSH (port 22)` → Linux access
            
        - `HTTP (port 80)` / `HTTPS (port 443)` → Web traffic
            
    - Outbound rules usually **allow all traffic** by default.
        

---

### 6️⃣ **(Optional) Add Storage**

- Add EBS volumes (default) or instance store.
    
- You can define size, volume type (gp3, io1, etc.), and whether it’s deleted on termination.
    

---

### 7️⃣ **(Optional) Add User Data**

- A **shell script** (Linux) or **PowerShell script** (Windows) that runs **on first boot only**.
    
- Used to automate setup:
    
    - Install software
        
    - Configure environment variables
        
    - Pull code from GitHub, etc.



**NOTE:** AS THE EC2, STOPS AND RESTRART THE PUBLIC IP CHANGES AUTOMATICALLY BY DEFAULT,BUT NOT THE PRIVATE IP (IT REMAINS SAME)


# types of instances

![[Pasted image 20251024184428.png]]