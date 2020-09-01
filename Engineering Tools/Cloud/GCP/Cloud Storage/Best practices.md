
# Best practices
- Ideal for storing and retrieving a large number of files, or store multiterabyte file exports and dumps of data for data analytics pipeline
- Storage classes
	- Multi-regional. Serving website content, Streaming videos, mobile apps
	- Regional. Data analytics
	- Nearline. Backup, serving long-tail and multimedia content
	- Coldline. Disaster recovery and data archiving. 
- Same bucket can have multi-regional+nearline+coldline or regional+nearline+coldline 
	- Rules can be applied to automatically migrate objects to a different storage class
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5Njc4NDIsMTcyNzA4NjE0MywtMTI0NT
Q4MTE0OSwtMTcwMzU2ODg3MV19
-->