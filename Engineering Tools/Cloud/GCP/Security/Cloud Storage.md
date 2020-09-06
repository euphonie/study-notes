# Security in Google Cloud Storage

- Control members who have access to organizations, folders, project or bucket and what access they have
- It is not possible to remove a permission at a lower level that was granted at a higher level.
- Predefined Roles
	- Storage Object Admin
		- get and list projects, CRUD objects get and set IAM policies
	- Storage Object Creator
		- get and list projects and create objects
	- Storage Object Viewer
		- get and list projects, get and list objects
- IAM permissions on buckets grant permission to a broad control over projects and buckets but not fine grain control over individual objects.
- ACLs can be used to grant access to objects in buckets. These are applied to individual buckets and individual objects.
	- Only required when needing fine grained control of buckets or objects
- IAM and ACLs can be both implemented
- **Use with caution** To make a bucket public grant `allUsers` the Storage Object Viewer
- **Use with caution** To make an object public, grant `allUsers` Reader access.

### Auditing Storage buckets
- Activity is logged automatically
- Includes operations that modify the config or metadata of a bucket or object
	- Data or access logs must be configured
		- Data includes operations that modify objects or read a project bucket or object
		- Data access log can be turned on at the bucket level

```bash
# Enabling data access logs
# Create a new bucket to hold the log files
gsutil mb gs://example-logs-bucket
# Allow write-access to the bucket for Cloud Storage Analytics
gsutil acl ch -g clou-storage-analytics@google.com:W gs://example-logs-bucket
# Set ACL of the logging bucket into project private
gsutil defacl set project-private gs://example-logs-bucket
# Enable logging and specify bucket holds logs with -b flag
gsutil logging set on -b gs://example-logs-bucket gs://example-bucket
```
**Export logs to BigQuery**

```python
# Create a BigQuery data set
bq mk storageanalysis
# load files to the BigQuery table
bq load --skip_leading_rows=1 storageanalysis.usage gs://example-logs-bucket/example-bucket_usage_2018_01_01_v0/cloud_storage_usage_schema_v0.json

bq load --skip_leading_rows=1 storageanalysis.storage gs://example-logs-bucket/example-bucket_usage_2018_01_01_v0/cloud_storage_usage_schema_v0.json
```

**Signed URLs and policy documents**
- For users that don't have google accounts
- Provide time-limited access for read and write to anyone in possession of the URL.
- Signed URLs can be created using gsutil
	1. Create a service account with desired rights
	2. Use the rights to generate the signed URL for storage object
	3. Create a key for the service account and store it in a file such as key.json.
	4. Use command to specify the service account key and object which permissions should be assigned
		- the -d parameter specifies the duration
- Policy Documents
	- specify what can be uploaded to a bucket with a form post
	- allow greater control over size, content type, and any other uploaded characteristics in comparison to signed URLs
	- Can be used by website owners to allow visitors to upload files to cloud storage
	- Constructed using JSON
	- Using a policy document for an HTML form post
		- correct a policy document with UTF-8 encoding
		- encode document as base64 
		- sign document using RSA with SHA-256 using the secret key provided in the Google Cloud Console. This creates the message digest
		- encode the message digest as a base64
		- add the policy document information to the HTML form

```bash
# manual creation of signed URLs
gsutil signurl -d 10m ~/key.json gs://super-secure-bucket/noir.png
```
**Using a policy document in an HTML form**
```html
<form action="http://travel-maps.storage.googleapis.com" method="post">
<input type="text" name="key" value="test-object">
<input type="hidden" name="Content-Type" value="image/jpeg">
<input type="hidden" name="success_action_redirect" value="https://www.example.com/success_notification.html">
<input type="hidden" name="policy" value="eyJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJ0cmF2ZWwtbWFwcyJ9LHsiY29udGVudC10eXBlIjoiaW1hZ2UvanBlZyJ9LHsic3VjY2Vzc19hY3Rpb25fcmVkaXJlY3QiOiJodHRwOi8vd3d3LmV4YW1wbGUuY29tL3N1Y2Nlc3Nfbm90aWZpY2F0aW9uLmh0bWwifSx7ImtleSI6InRlc3Qtb2JqZWN0In0seyJ4LWdvb2ctZGF0ZSI6IjIwMjAwMTIzVDA0MzUzMFoifSx7IngtZ29vZy1jcmVkZW50aWFsIjoiZXhhbXBsZV9hY2NvdW50QGV4YW1wbGVfcHJvamVjdC5pYW0uZ3NlcnZpY2VhY2NvdW50LmNvbS8yMDE5MTEwMi9hdXRvL3N0b3JhZ2UvZ29vZzRfcmVxdWVzdCJ9LHsieC1nb29nLWFsZ29yaXRobSI6IkdPT0c0LVJTQS1TSEEyNTYifV0sImV4cGlyYXRpb24iOiIyMDIwLTAxLTIzVDA0OjM1OjQwWiJ9">
<input type="hidden" name="x-goog-algorithm" value="GOOG4-RSA-SHA256">
<input type="hidden" name="x-goog-credential" value="example_account@example_project.iam.gserviceaccount.com/20191102/auto/storage/goog4_request">
<input type="hidden" name="x-goog-date" value="20191102T043530Z">
<input type="hidden" name="x-goog-signature" value="58bc39b8f604ee1f18171fee4828ef8967f3d2721676570e115d68c2f133820cbb833976f18955516b2b7d0c3d9660fea613a2ad90c240bd02c1eefa4a55e9038ce74dcfdd34e278ea0436e261131a36fa4e922f0a077ca1c9842f654928aac3ca7f9341075f9db275d8286b5ef13e7f91b4837e77b2a6dbea83f86b90f848331053d8a6b1fbc26787992e7fb819a2005bae9b3026b9c7d1158e88e4a2018f13757083c7873241d2dfe6ea46a17cd6f3d090f3e0da44ccfbd6bc425124de1bea744a32f3ab175672a991ef274cd83550eca57ea591b85fa9799098a38ec552dc3ec679c431491444820624f5c4ba0c8cf87d60af89899afce2a90325c6966dcf">

<input name="file" type="file">
<input type="submit" value="Upload">
</form>
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzM3ODcyOTldfQ==
-->