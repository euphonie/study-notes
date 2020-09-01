
# Best practices
- Ideal for storing and retrieving a large number of files, or store multiterabyte file exports and dumps of data for data analytics pipeline
- Storage classes
	- Multi-regional. Serving website content, Streaming videos, mobile apps
	- Regional. Data analytics
	- Nearline. Backup, serving long-tail and multimedia content
	- Coldline. Disaster recovery and data archiving. 
- Same bucket can have multi-regional+nearline+coldline or regional+nearline+coldline 
	- Rules can be applied to automatically migrate objects to a different storage class
- Strongly consistent operations
	- Read-after-write
	- Read-after-metadata-update
	- Read-after-delete
	- Bucket listing
	- Object listing
	- Granting access to resources
- Eventually consistent operations
	- Revoking access from objects
	- Accessing publicly readable cached objects

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1NTI5MDYxNiwtNDk2Nzg0MiwxNzI3MD
g2MTQzLC0xMjQ1NDgxMTQ5LC0xNzAzNTY4ODcxXX0=
-->