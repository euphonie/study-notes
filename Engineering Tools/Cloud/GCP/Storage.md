
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
- Objects are immutable. You don't edit them just create new versions.
- A geographic location is selected (region or multi-region)
- A class of storage is selected. There is a default storage class.
- **Access Control**
	- IAM policies are inherited from Project > Bucket > Object
	- Access Control Lists offer a finer control. They define who has access to the bucket and objects and what level of access they have.
		- Scope. Who can perform the specified action
			- 


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxNTM5ODk4NSwxNDY1MTM1OTE1LC0yMD
k5NDQyNzc4LDE1NjE2Mzg4OTEsLTE0MzEwNjUzNTldfQ==
-->