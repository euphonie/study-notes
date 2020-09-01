
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
	- Set CORS config in gsutil using a cors-config.json
		- `gsutil cors set gcs-cors-config.json gs://cords-demo-dar/`

```bash
# Make all files within a bucket public
gsutil -m acl set -R -a public-read gs://cords-demo-dar
```
**CORS example config**
```json
{
	{
		"origin": ["http://<webserver_ip>"],
		"responseHeader": ["*"],
		"method": ["*"],
		"maxAgeSeconds": 1
	}
}
```

**Naming conventions**
- Use globally unique bucket names
- Don't use personally identifiable information (PII)
- Use GUIDs if a lot of buckets are needed
- Don't use IP address noation
- Don't use google or misspelled names
- conform to standard DNS naming conventions

**Traffic**
- Consider operations per second/Bandwith/cache control
- Minimize spikes in traffic
- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY5MzI0MDY0NywxMjE3ODAxMzczLC0xNz
kwODAyNDE0LC05MjIyMTM3NTgsLTQ5Njc4NDIsMTcyNzA4NjE0
MywtMTI0NTQ4MTE0OSwtMTcwMzU2ODg3MV19
-->