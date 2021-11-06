
# Identity & Access Management

IAM lets administrators authorize who can take action on specific resources. Is conformed by: 
- **Who**
	-  User or users. Can be defined by:
		-  a Google Account
			- Represents a developer, administrator, or person who interacts with GCP
			- has a gmail user associated
		-  a Google Group
			- Named collection of google accounts and service accounts
			- has a unique email address
			- Don't have login credentials. Can't be used to establish identity to make a request to access a resource.
		-  a Service Account
			- Belongs to an application
		-  an entire G-Suite domain 
			- A virtual group of all the members in an organization
			- Can't be used to establish identity
			- Enable convenient permission management, like groups
		- or a Cloud Identity domain.
			- Virtual group of all members in an organization
			- Doesn't provide access to G Suite applications and features
- **Can do what**
	- Defined by an IAM role (a collection of permissions)
- **On which resource**

**Google Cloud Directory Sync**
- Synchronize LDAP or Microsoft Active Directory into Users an groups
- One-way only

**Single Sign-on**
- Use Cloud Identity to configure SAML SSO
- If SAML2 isn't supported, use a third-party solution (ADFS, Ping, or Okta)

## Permissions

Specify what operations are allowed on resources

Use the syntax
`<service>.<resource>.<verb>`

Ex. 
```
pubsub.subscriptions.consume
storage.objects.list
compute.disktypes.list
```

## Roles 

Collection of permissions. Grant roles to users, service accounts or groups.

- **Primitive**. Affect all resources in a project but might be too coarse when handling sensitive data. 
- Can be applied at project level using Cloud Platform console, API or G Cloud command line tool
- Owner role doesn't affect upwards, in an organization node you cannot modify organization's metadata but can modify projects under the organization
	- **Owner**
		- Invite members
		- Remove members
		- Delete Projects
		- Setup billing accounts (also Billing Project Manager role), add/remove permissions
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
	- More than one role can be applied to a user
- **Custom**. The most detailed setup for rules on resources. It can work along the concept of assigning the **least-privilege** needed actions to all users in an organization.
	- These can only be used at the project or organization levels, this means they can't be used at folder.

### Service Account

Is used to give permissions to server-to-server interactions or actions between services or resources.
These are identified with an email address, and instead of passwords use cryptographic keys. 

Service accounts can be used to allow certain levels of server-to-server interaction within the same project. For example having project A, with components 1 and 2. Service account 1 used by component 1 can edit project_b's configuration, but Service account 2 used by component 2 can't.

- Can be granted read access for a VM
- Can be
	- User-created (custom)
	- Built-in. CE and App Engine default service accounts
	- Google APIs service account. Runs internal Google processes on your behalf
- A service account can be assigned to a Compute Engine VMs, to authenticate with it when making calls to the Google API
	- If no service account is assigned, it needs to be manually configured
- Every GCP project has a default Service Account
- Can be created using IAM or Google Identity 
	- Roles need to be assigned
- User-managed service accounts do not use the access scope
	- Permissions are controlled through IAM roles
- Are associated with a key pair
- Can have up to 10 keys associated with them to facilitate key rotation (done daily by Google)
	- External keys can be created and used outside GCP

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

#### Create a service account
- Create the service account via the console
- Generate and download your credentials file
- Set an environment variable to provide credentials to your application
```bash
# linux or os x
export GOOGLE_APPLICATION_CREDENTIALS=<path_to_service_account_file>
# windows
set GOOGLE_APPLICATION_CREDENTIALS=<path_to_service_account_file>
```
- Authenticate in your code with the default credentials
```python
def implicit():
	from google.cloud import storage
	# There's no need to specify credentials as the constructor
	# will look for the environment variable
	storage_client = storage.Client()
	buckets = list(storage_client.list_buckes())
	print(buckets)
```
- Credentials are used to identify your application for quota and billing
- Applications check for credentials in the following order:
	- Google application credentials environment variable
	- Default service accounts, that CE, GKE or Cloud Functions provides
	- Error is thrown

## Organization

Google cloud is organized through the concept of projects, it can optionally be organized into folders. An organization can have multiple projects and within those projects folders and individual resources can be contained. Rules and permissions can be assigned to any element in this hierarchy. 
- Highly associated with a G Suite or Cloud Identity account
- Root node
- useful for auditing
- Project creator role can also be assigned at the organization level
- Folders can be used to assign policies, as all the resources in a folder inherit the IAM policies from the folder.
- All GCP resources belong to a project
- Each project is a separate compartment and each resource belongs to exactly one
- Project's ID are user-defined, unique and immutable
	- GCP assigns a name and an unique project number
- **Super administator role**
	- Can
		- Assign the organization admin role to some users
		- Be the point of contact in case of recovery issues
		- Control the lifecycle of the GSuite or Cloud Identity account and Organization Resources

### Organization Node

Allows having centralized visibility on how the resources are being used, and also permits applying centralized policies on all the projects that belong to an organization. It's the top of the hierarchy. It contains two main roles: 

- **Organization Policy Administrator**. Broad control over resources, makes it necessary for people to have the privilege in order to change policies.
	- Can
		- Define IAM policies
		- Determine the structure of the resource hierarchy
		- Delegate responsibility over critical components such as Networking, Billing and Resource Hierarchy through IAM roles
- **Project Creator**. Fine-grained control of project creation. A way to control who can spend money.
- **Viewer role**
	- View access to all resources

To be able two have an organization node there can be two ways:
- You're an owner of a G-Suite account
- Using Google Cloud Identity for creating an organization node.

*Note*: Child policies cannot restrict access granted at the parent level.

## Folders
- Can be view as sub organizations within the organization
- Provide additional grouping mechanisms and isolation boundaries between projects
- Can model different legal entities, departments, and teams within a company.
- Hierarchy could be 
	- Departaments
		- Teams
			- Products
- Allow delegation of administration rights
- Access can be limited by a folder
- Roles
	- Admin. Full control over folders
	- Creator. Browse hierarchy and create folders
	- Viewer. View folders and projects below a resource

## Project
- Roles
	- Creator. Create new projects (automatic owner) and migrate new projects into organization
	- Deleter. Delete projects

## Cloud IAM policy

Represented by the policy object. A policy consists of a list of bindings. A binding binds a list of members to a role.
- Methods
	- setIAMPolicy(). set policies.
	- getIAMPolicy(). get a policy that was previously set.
	- testIAMPermissions(). test whether the caller has the specified permissions for a resource.

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

# Best practices
- Follow the principles of least privilege. Grant at the smaller scope needed.
- Rotate service account keys
- Manage user-managed service account keys
- Don't check in service account keys to source code
- Use Cloud Audit Logging and export logs to Cloud Storage to monitor changes to policies
- Set organization-level IAM policies
- Grant roles to a Google group when possible
	- Update group membership instead of changing Cloud IAM policy
	- Audit membership of groups used in policies
	- Control the ownership of the Google group used in Cloud IAM policies
- Using Service Accounts
	- use different service accounts for different functions
	- Be very careful grating serviceAcountUser role
	- When you create a service account, give it a display name that clearly identifies its purpose
	- Establish a naming convention for service accounts
	- Establish key rotation policies and methods
	- Audit with serviceAccount.keys.list() method
- use custom roles sparingly
- Use projects to group resources that share the same trust boundary
- Audit policies in Cloud audit logs: `setiampolicy`
- Audit membership of groups used in policies
- permissions can't be assigned to identities
- Define a resource hierarchy
- Use pre-defined roles preferably

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMjcwMDk3NzYsLTEzNTg2MzAwNDAsMT
Q0OTQzMDg2OCwtMTc2ODg4NzY4NSwyOTU3OTcxNzMsLTU1OTU0
NDA4NCwxNjc0MjM2MzE1LC0xOTU3MTM3OTU2LDE4Njk2NTc3Nj
UsLTExNDIxOTgxODZdfQ==
-->