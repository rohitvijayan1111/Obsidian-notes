
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