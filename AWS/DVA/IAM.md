
Topics Covered:
* Aws Regions, Az, AWS Points of Presence (Edge Locations)

# IAM

AWS Account
 └── IAM (Global)
      ├── Users ──> can belong to → Groups
      ├── Groups ──> have Policies
      ├── Roles ──> assumed by entities/services
      ├── Policies:
      │    ├── AWS Managed
      │    ├── Customer Managed
      │    └── Inline
      └── Resource-based Policies (attached directly to resources)


Policy format:

```
{
id:
version:
statement:
{
sid:
effect: -> Allow / Deny permission
actions:[] -> the actions that could be done(api calls)
principal -> For whom and all this policy is applied   // (Only in resource-based policies)
resource: -> policy on which resource
}}
```

Permission Boundary:
A **permissions boundary** says:

> “Even if a user’s policies say _Allow_, they can only perform actions that are also _Allowed_ by the boundary.”
> 

If a user has **AdministratorAccess** but a **permissions boundary** allowing only S3 actions,  
➡️ the user can access **only S3** — because the **boundary limits** what the policy can grant.  
🧠 **Final permission = intersection of user policy and boundary; boundaries never grant extra access.**


- HOW To open an user account in aws??

## IAM Roles
• Some AWS service will need tc perform actions on your behalf
• To do so, we will assign permissions to AWS services with IAM Roles

### Creating IAM Roles

## 🧩 **How to Create an IAM Role**

### 🖥️ **From AWS Management Console**

1. **Sign in** to the **AWS Management Console**.
    
2. Go to **IAM → Roles → Create role**.
    
3. **Select the trusted entity type** (who or what will assume this role):
    
    - **AWS Service** → e.g., EC2, Lambda, etc.
        
    - **Another AWS account** → for cross-account access.
        
    - **Web identity / SAML federation** → for external users (Cognito, Google, etc.).
        
4. **Select the specific use case** (e.g., _EC2_ if attaching to an EC2 instance).
    
5. **Attach policies** to define permissions — e.g.:
    
    - `AmazonS3FullAccess`
        
    - `CloudWatchLogsFullAccess`
        
6. (Optional) Add **tags** for identification.
    
7. Give the role a **name and description** → e.g., `EC2_S3Access_Role`.
    
8. Click **Create role** ✅
# MFA


 Types:
 - Virtual MFA
 - U2F(Universal two factor) security key
 - Hardware Key Fob MFA Device


## 🧩 **How to Configure AWS MFA (Multi-Factor Authentication)**

### 🔧 Steps:

1. **Sign in** to the **AWS Management Console** as the IAM user or root user.
    
2. Go to **IAM → Users → [Your Username] → Security Credentials** tab.
    
3. Under **Multi-Factor Authentication (MFA)**, click **“Assign MFA device.”**
    
4. Choose the device type:
    
    - **Virtual MFA device** (recommended) – e.g., Google Authenticator, Authy, or AWS Virtual MFA App.
        
    - **Hardware key/fob** – physical MFA device like YubiKey.
        
5. Scan the QR code using your MFA app.
    
6. Enter **two consecutive MFA codes** displayed on your app.
    
7. Click **“Add MFA”** — setup complete ✅


# Types of AWS Access

- AWS Management Console (protected by password + MFA)
-  AWS Command Line Interface (CLI): protected by access keys 
- AWS Software Developer Kit (SDK) - for code: protected by access keys



## 🧩 **How to Configure AWS CLI + Create Access Keys**

### 🪪 **Part 1: Create Access Keys (for CLI use)**

1. **Sign in to AWS Console** → as your **IAM User** (not root ideally).
    
2. Go to **IAM → Users → [your username] → Security Credentials** tab.
    
3. Scroll to **Access keys** section → click **“Create access key.”**
    
4. Choose the **use case** (e.g., “Command Line Interface (CLI)”).
    
5. AWS will generate:
    
    - **Access key ID**
        
    - **Secret access key** (shown only once — copy it safely)
        
6. Store them in a secure place (e.g., AWS Secrets Manager or password vault).
    

---

### 💻 **Part 2: Configure AWS CLI**

1. Open your terminal or command prompt.
    
2. Run:
    
    `aws configure`
    
3. Enter details when prompted:
    
    `AWS Access Key ID [None]: <your access key> AWS Secret Access Key [None]: <your secret key> Default region name [None]: ap-south-1 Default output format [None]: json`


## AWS Cloud Shell

- It is a feature in AWS Cloud management console, that is used to create CLI session via the browser itself.
- It is only available in a few Regions.





# IAM Security Tools


• IAM Credentials Report (account-level)
• a report that lists all your account's users and the status of their various
credentials
• IAM Access Advisor (user-level)
• Access advisor shows the service permissions granted to a user and when those
services were last accessed.


# IAM Guidelines 

• Don't use the root account except for AWS account setup
• One physical user = One AWS user
• Assign users to groups and assign permissions to groups
• Create a strong password policy
• Use and enforce the use of Multi Factor Authentication (MFA)
• Create and use Roles for giving permissions to AWS services
• Use Access Keys for Programmatic Access (CLI / SDK)
• Audit permissions of your account using IAM Credentials Report & IAM
Access Advisor
• Never share IAM users & Access Keys

![[Pasted image 20251023224336.png]]