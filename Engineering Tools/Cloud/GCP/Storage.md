
# Storage Options

- VMs come with persistent disks.

## NoSQL Databases

### Bigtable

- Fully managed NoSQL, wide-column database service for terabyte applications

### Datastore
### Firestore

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
- Ways to upload data into Cloud Storage
	- Online transfer
		- Self-managed copies using command-line tools or drag-and-drop (Chrome browser)
		- **gsutil**, the cloud storage command from Cloud SDK
	- Online Storage Transfer Service
		- Scheduled, managed batch transfers
		- Storage from another cloud provider, different cloud storage region or from an HTTPS endpoint
	- Offline Transfer Appliance
		- Rackable appliances that are leased from Google to securely ship your data
		- Securely transfer up to 1 petabyte of data on a single appliance
- Importing from other GCP services
	- BigQuery. import and export tables
	- Compute Engine. startup scripts, images, and general object storage
	- Cloud SQL. import and export tables
	- App Engine. Object storage (images), logs, and datastore backups

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
	- Accessible from the cloud storage API
	- The lower accessed type of storage the lower the price is per GB stored per month and the higher the price per GB transferred.
	- **Multi-regional**. Most frequently accessed. SLA 99.95%. Used for CDNs. Geo-redundant, data is stored in two geographic locations separated at least by 160 kilometres.
		- Website content, interactive content and data for mobile and gaming applications
	- **Regional**. Accessed frequently within a region. SLA 99.90%. Used for in-region analytics, transcoding. **Stores in specific GCP region** Cheaper than multi-regional but less redundancy.
		- Data near the CE VMs for better performance in data-intensive computations.
	- **Nearline**. Accessed less than once a month. SLA 99%. Long-tail content, backups
		- Continuously add files and analyze them all at the end of the month
	- **Coldline**. Accessed less than once a year. SLA 99%. Archiving, disaster recovery. 90-day minimum storage duration
- **Access Control**
	- IAM policies are inherited from Project > Bucket > Object
	- Access Control Lists offer a finer control. They define who has access to the bucket and objects and what level of access they have.
		- Scope. Who can perform the specified action
			- User or group of users 
		- Permission. What actions can be performed
			- Ex. Read or write


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwMjQyOTgzNiwxMTg4OTg4MjY1LDU3MD
AwODYyMSwtMTg4MTEyMDcxNSwxNDY1MTM1OTE1LC0yMDk5NDQy
Nzc4LDE1NjE2Mzg4OTEsLTE0MzEwNjUzNTldfQ==
-->