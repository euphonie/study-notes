
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
- BigQuery
	- Leverage IAM roles to comply with restrictions
	- Separate who can create and manage datasets vs who can query and process the data
	- Principle of least privilege
	- Set the default table exploration for new created tables in a data set. If property is set, any table created in the dataset is deleted after the expiration period.
	- If property is set after the dataset is created, only new tables are deleted after the expiration period

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjAwMzc1NzYwXX0=
-->