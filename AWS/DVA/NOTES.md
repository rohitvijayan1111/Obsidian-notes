
Topics Covered:
* Aws Regions, Az, AWS Points of Presence (Edge Locations)


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

