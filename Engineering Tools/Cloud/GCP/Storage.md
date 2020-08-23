
# Storage Options

- VMs come with persistent disks.

## NoSQL Databases
- Bigtable
- Datastore
- Firestore

## Relational Databases
- Cloud SQL
	- PostgreSQL
	- MySQL
	- Microsoft SQL Server
- Cloud Spanner

## File System
- Filestore

## Object System

### Cloud Storage 

Works for object storage. It relates group of bytes with an unique key for addressing it.

- Comprised by buckets. Unstructured data and files.
	- May contain
		- Files 
		- Folders
		- Objects 
- Is not a filesystem.
- Encrypts data at rest and in transit (HTTPS)
- High performance, internet-scale
- Objects stored with high durability and high availability
- Simple administration
	- No need to provision capacity ahead of time
- Each object is assigned an unique key in the form of an URL
- Fully managed and scalable service
- Uses:
	- Serving website content
	- Storing data for achival and disaster recovery
	- Distributing large data objects via Direct Download

#### Buckets
- Has a globally unique name
- Created and configured by user
- Object versioning can be turned on, keeping a history of modifications.
	- Deletes or overrides objects in the bucket
	- Archived versions can be restored or permanently deleted
	- Lifecycle management policies can be used to avoid cluttering the bucket with old versions of an object
		- Ex. Delete objects older than 365 days
			- Keep only latest 3 versions of the objet
	- **Without object versioning**, new objects always override old objects
- Objects are immutable. You don't edit them just create new versions.
- A geographic location is selected (region or multi-region)
- A class of storage is selected. There is a default storage class.
	- The lower accessed type of storage the lower the price is per GB stored per month
	- **Multi-regional**. Most frequently accessed. SLA 99.95%. Used for CDNs
	- **Regional**. Accessed frequently within a region. SLA 99.90%. Used for in-region analytics, transcoding
	- **Nearline**. Accessed less than once a month. SLA 99%. Long-tail content, backups
	- **Coldline**. Accessed less than once a year. SLA 99%. Archiving, disaster recovery
- **Access Control**
	- IAM policies are inherited from Project > Bucket > Object
	- Access Control Lists offer a finer control. They define who has access to the bucket and objects and what level of access they have.
		- Scope. Who can perform the specified action
			- User or group of users 
		- Permission. What actions can be performed
			- Ex. Read or write


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMDYxOTE2MjAsNTcwMDA4NjIxLC0xOD
gxMTIwNzE1LDE0NjUxMzU5MTUsLTIwOTk0NDI3NzgsMTU2MTYz
ODg5MSwtMTQzMTA2NTM1OV19
-->