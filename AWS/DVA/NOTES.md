
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