
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
	- Buckets have globally unique names
	- Created and configured by the user
	- Objects are immutable. You don't edit them just create new versions.
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


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTk0NDI3NzgsMTU2MTYzODg5MSwtMT
QzMTA2NTM1OV19
-->