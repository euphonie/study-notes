
# Storage Options

## Summary

![Storage Options](https://raw.githubusercontent.com/euphonie/study-notes/master/Engineering%20Tools/Cloud/GCP/storageoptions.png)

![Storage Options: cont.](https://raw.githubusercontent.com/euphonie/study-notes/master/Engineering%20Tools/Cloud/GCP/techdetails.png)

- VMs come with persistent disks.

## NoSQL Databases

### Bigtable

- Fully managed NoSQL, wide-column database service for terabyte applications
- Can scale up to billion of rows and thousands of columns
- Ideal for data that has a single lookup key
- Can also be viewed as a persistent hash table
- High throughput and low latency. Great for IoT, user analytics and financial data analysis.
- Accessed using open source HBase API (native database for Apache Hadoop)
- Native compatibility with big data, Hadoop ecosystems
- It's managed, increasing machine count doesn't require downtime
	- Administration tasks are also handled, upgrades and restarts transparently
- Data encrypted in-flight and at rest
- IAM permissions can be set to control who has access to Bigtable data
- **Access Patterns**
	- Application API. Data can be accessed through a data service layer, HBase REST server, or a java server with HBase client.
	- Streaming. Data can be streamed in through Cloud Dataflow Streaming, Spark Streamlining and Storm
	- Batch Processing. Data can be read from and written through Hadoop's Map Reduce, Dataflow or Spark batch processes. 

### Datastore

Horizontally scalable NoSQL DB
- Fully managed service
	- Automatically handles sharding and replication
- Handles transactions
- Lets issue SQL-like queries
- Main use case is to store structured data from App Engine apps. 
- Designed for application backends
- Integration point for applications using App Engine and Compute Engine
- Free tier with a daily quota of storage, reads, writes, deletes and small operations

### Firestore

## Relational Databases

### Cloud SQL

- Provides Terabytes of capacity
- Managed RDBMS
- A Database server could also be run inside a Compute Engine VM
- Cloud SQL provides replica services, read, failover, and external replicas
- Offers backup with on-demand or scheduled criteria
- Horizontal scaling (read replicas) Vertical scaling (changing machine type)
- Security
	- Includes network firewalls, data encrypted while on Google's network, encrypted whle stored in database tables, temporary files, and backups
- Options
	- PostgreSQL
	- MySQL
	- Microsoft SQL Server
- Integrations
	- App Engine. using standard drivers, a Cloud SQL can follow an App Engine application
	- Compute Engine. can be authorized to access Cloud SQL instances using an external IP addresses. Cloud SQL instances can be configured with a preferred zone
	- External services. Can be used with external applications and clients, external read replicas can be configured.
		- SQL Workbench, Toad

### Cloud Spanner

A horizontally scalable RDBMS
- Provides petabytes of capacity
- Offers transactional consistency on a global scale, schemas, automatic synchronous replication 
- Managed instances with high availability
- This should be looked into if relational databases or sharding has been outgrown, there's a need for transactional consistency, global data and strong consistency or to consolidate your database
	- Use cases: financial applications, and inventory applications

### BigQuery

- Big data analysis and interactive query and capabilities
- Relational SQL for OLAP
- Doesn't offer transactions
- Offers complex queries
- Provides petabytes of capacity

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
eyJoaXN0b3J5IjpbLTExNTExODIwNTcsLTExMjY4MjQyNjMsMT
M4MjUyMDkyNCwxNTgyMDAzODY3LDExODg5ODgyNjUsNTcwMDA4
NjIxLC0xODgxMTIwNzE1LDE0NjUxMzU5MTUsLTIwOTk0NDI3Nz
gsMTU2MTYzODg5MSwtMTQzMTA2NTM1OV19
-->