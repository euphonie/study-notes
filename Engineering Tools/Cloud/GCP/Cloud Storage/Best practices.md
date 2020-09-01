
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
- CNAME redirects
- Composite objects and parallel uploads
- Applications should be designed using truncated exponential backoff for network failures for HTTP responses 5xx and 429 codes
- Enable CORS
	- Make files within a bucket public
	- 
```bash
# Make all files within a bucket public
gsutil -m acl set -R -a public-read gs://cords-demo-dar
```
**CORS config**
```json
{
	{
		"origin": ["*"],
		"responseHeader": ["*"],
		"method"
	}
}
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIxNzgwMTM3MywtMTc5MDgwMjQxNCwtOT
IyMjEzNzU4LC00OTY3ODQyLDE3MjcwODYxNDMsLTEyNDU0ODEx
NDksLTE3MDM1Njg4NzFdfQ==
-->