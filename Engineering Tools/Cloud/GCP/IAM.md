
# Identity & Access Management

IAM lets administrators authorize who can take action on specific resources. Is conformed by: 
- **Who**
	-  User or users. Can be defined by:
		-  a Google Account
			- Represents a developer, administrator, or person who interacts with GCP
		-  a Google Group
			- Named collection of google accounts and service accounts
			- has a unique email address
		-  a Service Account
			- Belongs to an application
		-  an entire G-Suite domain 
		- or a Cloud Identity domain.
- **Can do what**
	- Defined by an IAM role (a collection of permissions)
- **On which resource**

## Roles 

- **Primitive**. Affect all resources in a project but might be too coarse when handling sensitive data. 
	- **Owner**
		- Invite members
		- Remove members
		- Delete Projects
		- Setup billing, add/remove permissions
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
- **Predefined**. Can be applied on **Compute Engine** resources in a project, folder or organization. Provides more finer-grained rules on access and control over resources.
- **Custom**. The most detailed setup for rules on resources. It can work along the concept of assigning the **least-privilege** needed actions to all users in an organization.
	- These can only be used at the project or organization levels, this means they can't be used at folder.

### Service Account

Is used to give permissions to server-to-server interactions or actions between services or resources.
These are identified with an email address, and instead of passwords use cryptographic keys. 

Service accounts can be used to allow certain levels of server-to-server interaction within the same project. For example having project A, with components 1 and 2. Service account 1 used by component 1 can edit project_b's configuration, but Service account 2 used by component 2 can't.

- A service account can be assigned to a Compute Engine VMs, to authenticate with it when making calls to the Google API
	- If no service account is assigned, it needs to be manually configured
- Every GCP project has a default Service Account
- Can be created using IAM or Google Identity 
	- Roles need to be assigned
- User-managed service accounts do not use the access scope
	- Permissions are controlled through IAM roles

**Default service account has Project Editor Role which can be dangerous, as it can delete resources**

- Access scope still has to be created for a default service account
	- Access scope exists only for the instance lifetime

*Note*. A service account is also a resource, and can have IAM policies on its own attached to it.

#### Access scopes

- Allow default access
	- Narrow, allows read-only access to storage and Stackdriver Logging and monitoring.
	- Security error when trying to access any other Google API
		- Ex. Access to BigQuery, Datastore, Cloud SQL, Cloud Pub Sub or Cloud Bigtable
- Allow full access to all Cloud APIs
	- Bad practice as it does not follow the principle of least privilege
- Set access for each API
	- Only some Google API services 


## Organization

Google cloud is organized through the concept of projects, it can optionally be organized into folders. An organization can have multiple projects and within those projects folders and individual resources can be contained. Rules and permissions can be assigned to any element in this hierarchy. 
- Folders can be used to assign policies, as all the resources in a folder inherit the IAM policies from the folder.
- All GCP resources belong to a project
- Each project is a separate compartment and each resource belongs to exactly one
- Project's ID are user-defined, unique and immutable
	- GCP assigns a name and an unique project number

### Organization Node

Allows having centralized visibility on how the resources are being used, and also permits applying centralized policies on all the projects that belong to an organization. It's the top of the hierarchy. It contains two main roles: 

- **Organization Policy Administrator**. Broad control over resources, makes it necessary for people to have the privilege in order to change policies.
- **Project Creator**. Fine-grained control of project creation. A way to control who can spend money.

To be able two have an organization node there can be two ways:
- Your an owner of a G-Suite account
- Using Google Cloud Identity for creating an organization node.

*Note*: Higher-level policies (resource-level) can't take away access that's granted at a lower level (organization node level).

## Organization Policies

Centralized and programmatic control over organization's cloud resources. A policy administrator can configure restrictions across the entire resource hierarchy.
- Configure restrictions on how your organization's resource can be used
- Define and establish guard rails for dev teams to stay within compliance boundaries
- Assist product owners and teams to move quickly without breaking compliance

- To define a policy
	- Choose a constraint (particular type of restriction against GCP service or group of services)
	- Configure that constraint
	- Descendants inherit the organization's policy

- Constraint
	- Blueprint that defines what behaviors are controlled
	- Two main types
		- List 
			- Allows or disallows values within a list
			- Ex. compute.vmExternalIpAccess. This applies to all CE VM instances that have external IP access
		- Boolean
			- Turn policies on or off
			- Ex. compute.disableSerialPortAccess
- A use case is allowing users to only create boot disks with Trusted Images in the organization.


# Snippets

```bash
# Get list of accounts
gcloud auth list
# Get list of projects
gcloud config list project
# Create a service account
gcloud iam service-accounts create my-sa-123 --display-name "my service account"
# Add a policies and role to a service account
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \ --member serviceAccount:my-sa-123@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/editor
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxNDI2NzgyMiwtMjA5NTg3NDIyMSwxOD
U3MzU1Mzk4LC0xMDA0ODQ5NDA4LDE3NTQ1NzQ2NDcsLTExMTc4
ODA1MzcsMTI4NTkxOTkzMywxMzU1NjY2MjY5LC00NTUyMTk4NT
csLTEyMzE3MjM0NjNdfQ==
-->