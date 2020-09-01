
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
- Consider operations per second/Bandwith/cache control (read freq migh be lower)
- Minimize spikes in traffic
- Spread updates throughout the day
- Use exponential backoff on errors
- When write req/sec > 1000 or read req/sec > 5000
	- Start with a request rate below or near the threshold
	- Double the request rate no faster than every 20 minutes

**Location**
- Store data in a region closest to your application's users 
- Consider region specific compliance requirements
- For analytical workloads store the data in regional buckets to reduce network charges and better performance compared to multi-region
- Multi-regional and regional storage
	- Provide the best availability
	- Are good options for data served at a high rate with high availability
- Nearline and coldline
	- Infrequently accessed data
	- Data that tolerates slightly lower availability

**Security**
- IAM
	- Access to buckets
	- Bulk access to a bucket's objects
- ACL
	- Read or write access to users for individual buckets or objects
	- Access when fine-grained control over individual objects is required
- Signed URLs
	- Provide time-limited read or write access to an object, through a generated URL
	- Can be created using gsutil or programmatically
- Signed Policy Documents
	- Specify what can be uploaded to a bucket
	- Control size, content type, and other upload characteristics
- Firebase Security Rules
	- Granular, attribute-based access control to mobile and web apps using the Firebase SDKs for Cloud Storage
- Always use TLS (HTTPS) when transporting data
- Use HTTPS library that validates server certificates
- Revoke auth credentials to applications that no longer need access
- Securely store credentials
- Use groups instead of large numbers of users
- Bucket and object ACLs are independent of each other
- Avoid making buckets
	- Publicly readable or writable
- For XMLHttpRequests, XHR callbacks to get progress updates or if it's stalled
	- Don't close and re-open the connection. It creates a bad positive feedback loop during times of network congestion
- Set reasonably long timeouts for upload traffic

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyMDk0NDkzNiw2NDk3MjE4MiwtNjY2MT
QzNzMwLC0xMjIyMTA1Mzc3LC02MzMzNjc1OTcsMTIxNzgwMTM3
MywtMTc5MDgwMjQxNCwtOTIyMjEzNzU4LC00OTY3ODQyLDE3Mj
cwODYxNDMsLTEyNDU0ODExNDksLTE3MDM1Njg4NzFdfQ==
-->