
# Identity & Access Management

IAM lets administrators authorize who can take action on specific resources. Is conformed by: 
- Who
	-  User or users. Can be defined by a Google Account, a Google Group, a Service Account, an entire G-Suite or a Cloud Identity domain.
- Can do what
	- Defined by an IAM role (a collection of permissions)
- On which resource

## Roles 

- Primitive
- Predefin

## Organization

Google cloud is organized through the concept of projects. An organization can have multiple projects and within those projects folders and individual resources can be contained. Rules and permissions can be assigned to any element in this hierarchy. 
- Folders can be used to assign policies, as all the resources in a folder inherit the IAM policies from the folder.

Allows having centralized visibility on how the resources are being used, and also permits applying centralized policies on all the projects that belong to an organization. It's the top of the hierarchy. It contains two main roles: 

- **Organization Policy Administrator**. Broad control over resources, makes it necessary for people to have the privilege in order to change policies.
- **Project Creator**. Fine-grained control of project creation. A way to control who can spend money.

To be able two have an organization node there can be two ways:
- Your an owner of a G-Suite account
- Using Google Cloud Identity for creating an organization node.

*Note*: A less restrictive parent policy overrides a more restrictive resource policy.
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzMjMzNDcxNywtMTIzMTcyMzQ2M119
-->