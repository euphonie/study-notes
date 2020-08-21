
# Identity & Access Management

IAM lets administrators authorize who can take action on specific resources. Is conformed by: 
- Who
	-  User or users. Can be defined by a Google Account, a Google Group, a Service Account, an entire G-Suite or a Cloud Identity domain.
- Can do what
	- Defined by an IAM role (a collection of permissions)
- On which resource

## Roles 

- **Primitive**. Affect all resources in a project but might be too coarse when handling sensitive data. 
	- **Owner**
		- Invite members
		- Remove members
		- Delete Projects
		- +editor, viewer
	- **Editor**
		- Deploy applications
		- Modify code
		- Configure services
		- +viewer
	- **Viewer**
		- Read-only access
	- **Billing Administrator**
		- Manage billing
		- Add and remove administrators
- **Predefined**. Can be applied on Compute Engine resources in a project, folder or organization. Provides more finer-grained rules on access and control over resources.
- **Custom**. The most detailed setup for rules on resources. It can work along the concept of assigning the **least-privilege** needed actions to all users in an organization.
	- These can only be used at the project or organization levels, this means they can't be used at folder.

### Service Account

Is used to give permissions to server-to-server interactions or actions between services or resources.
These are identified with an email address, and instead of passwords use cryptographic keys. 

Service accounts can be used to allow certain levels of server-to-server interaction within the same project. For example having project A, with components 1 and 2. Service account 1 used by component 1 can edit project_b's configuration, but Service account 2 used by component 2 can't.

*Note*. A service account is also a resource, and can have IAM policies on its own attached to it.

## Organization

Google cloud is organized through the concept of projects, it can optionally be organized into folders. An organization can have multiple projects and within those projects folders and individual resources can be contained. Rules and permissions can be assigned to any element in this hierarchy. 
- Folders can be used to assign policies, as all the resources in a folder inherit the IAM policies from the folder.
- All GCP resources belong to a project
- Each project is a separate compartment and each resource belongs to exactly one
- Project's ID are user-defined, unique and immutable
	- GCP assigns a name and an unique project number

Allows having centralized visibility on how the resources are being used, and also permits applying centralized policies on all the projects that belong to an organization. It's the top of the hierarchy. It contains two main roles: 

- **Organization Policy Administrator**. Broad control over resources, makes it necessary for people to have the privilege in order to change policies.
- **Project Creator**. Fine-grained control of project creation. A way to control who can spend money.

To be able two have an organization node there can be two ways:
- Your an owner of a G-Suite account
- Using Google Cloud Identity for creating an organization node.

*Note*: Higher-level policies can't take away access that's granted at a lower level.
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1MTMzNDk2NSwxNzU0NTc0NjQ3LC0xMT
E3ODgwNTM3LDEyODU5MTk5MzMsMTM1NTY2NjI2OSwtNDU1MjE5
ODU3LC0xMjMxNzIzNDYzXX0=
-->