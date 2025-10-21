
Topics Covered:
* Aws Regions, Az, AWS Points of Presence (Edge Locations)


IAM

- Global configured not limited to one region
- IAM Has :
	- Users
	- Groups
	- Roles
	- Policies
		- Inline Policy


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