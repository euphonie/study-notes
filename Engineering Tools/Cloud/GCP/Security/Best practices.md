
# Best practices

- Cloud Storage
	- Don't use personally identifiable information (PII) in bucket names
	- Names must be unique on the entire Cloud storage namespace
	- If a lot of buckets are needed use GUIDs for bucket names plus retry logic in case of collisions and keep a cross reference
	- Don't use PII in object names 
	- Check default object ACLs on buckets
	- Use signed URLs for users with no google account
	- Don't allow buckets to be publicly writable
	- Use lifecycle rules to remove sensitive data no longer needed
	- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3Njg1ODY4NzJdfQ==
-->