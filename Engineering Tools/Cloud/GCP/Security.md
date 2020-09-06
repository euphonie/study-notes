# Security


## Connection to Virtual Machines

- Linux instances accessed via Secure Shell 
	- Require a username and an SSH key
	- Password authentication is disabled by default
	- GCP console provides built-in SSH access
		- Connects through HTTPS and shares SSH keys to initiate an SSH session
		- Needs public IP address and a firewall rule for incoming TCP traffic in port 22
		- GCloud SDK can also be used `gcloud compute ssh web-server --zone us-central1-c`
			- This process automatically locates .ssh keys in ~/.ssh
- Connecting from outside Google Console
	- Is possible with a username and valid SSH key
		- Key needs to be provided to the instance using the project's metadata `SSH Keys` tab
- VMs can be configured to not use project-wide SSH keys `Block project-wide SSH keys`
- Keys can also be added to instance-specific metadata
- **If no public address**
	- Bastion host
		- Create a second VM with public IP in the same network
		- Connect to Bastion host
			- Bastion host should have rules limiting hosts that can connect and the private instance should only allow SSH traffic from the Bastion host
		- SSH into private VM
- Window instances accessed via Remote Desktop Protocol
	- Require username and password
	- Password is set using the dropdown next to the RDP button. GCloud command is `gcloud compute reset <windows_password> <instance_name> <user_name>`
	- RDP connects to the external address of the instance
	- Password is automatically generated the first time, a new password needs to be set up

**Using Shielded VMs**

- Protects workloads from remote attacks, privilege escalation, and malicious insiders
	- Protect against advanced threats
	- Ensure workloads are trusted and verifiable
		- Be sure instances haven't been compromised by boot level or kernel level malware or rootkits
	- Protect secrets against replay and exfiltration
	- Secure boot prevents loading of malicious code during bootup
		- Accomplished using UEFI firmware
		- Code that is not properly signed or unsigned at all, isn't allowed to run.
	- Measured boot checks for modified components during bootup
		- Hashes components to keep track of the quantity and sequence order (Integrity Monitoring)
		- Using a virtualized Trusted Platform Model (vTPM)
			- Virtualized version of a specialized computer chip. It creates a boot baseline known as Integrity Policy Baseline
- Creates logged events so they can be monitored using Stackdriver
	- clearTPMEvent. If the vvTPM has been cleared and deletes any secrets 
	- earlyBootReportEvent. If the early boot sequence integrity check passed
	- lateBootReportEvent. If the late boot sequence integrity check passed
	- setShieldedInstanceIntegrityPolicy. When integrity policy baseline is updated
	- shutdownEvent. When the VM instance is stopped.
	- startupEvent. When the VM instance is started (A track is kept for how many times the VM instance has been restarted)
	- updateShieldedInstanceConfig. When one of the shielded VM options is enabled or disabled
- VM Options
	- CentOS7
	- Container-Optimized OS 69+
	- RedHat Enterprise 7
	- Ubuntu 16.04 and 18.04 LTS
	- Windows Server 2012 R2, 2016, 2019

## Encrypting Disk

- GCP encrypts any data at rest without any action required
	- Keyczar is used
	- Includes data in Cloud Storage, CE persistent disks, CE VMs, disk snapshots and Cloud SQL Databases
- Process
	- All data is encrypted with a unique data encryption key or deck
	- Data is separated into chunks and encrypted with its own key. Key is not shared by two chunks
	- Data chunks are then distributed across Google's storage infrastructure
- Data chunks are encrypted with DEK and stored with wrapped DEK
- Keys are stored and used inside Google's Central Key Management Service or KMS
	- These are backed up and indefinitely recoverable
- Google KMS retrieves the unwrapped DEK when requested, with which the data chunk can then be decrypted
- The process is enabled by default and managed by Google
- Key rotation schedule is applied every 90 days to KEKs
	- Google stores up to 20 versions of the keys
	- Re-encryption of data is required at least once every 5 years
- **Optional** Users can also choose to managed their own keys
	- Allows to set keys, rotation periods, keys expiration
	- Keys are still stored in Google KMS
	- Keys belong to a key ring and a key resides in a particular location (regional, multi-regional or global)
	- KMS supports symmetric and asymmetric key types
	- Keys should be assigned when creating resources and the service accounts should also be granted permissions to use the keys
- With customer supplied keys Google does not store the keys, customer is then responsible for all key management and rotation. Data can be lost if the keys are lost as well
	- And key must be specified each time a resource is started or created

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

# Security in BigQuery

- BigQuery uses IAM for resources and permissions
- Tables, rows and columns are child resources of datasets and inherit their permiss

# Snippets

```bash
# Create a key
openssl rand 32 > mykey.txt
# Verify key
more mykey.txt

# Download Google CE public certificate
curl \ https://cloud-certs.storage.googleapis.com/google-cloud-csek-ingress.pem \ > gce-cert.pem
# Extract public key from the certificate
openssl x509 -pubkey -noout -in gce-cert.pem > pubkey.pem
# RSA-wrap the custom key 
openssl rsautl -oaep -encrypt -pubin -inkey pubkey.pem -in \ mykey.txt -out rsawrappedkey.txt
# Encode the RSA-wrapped key in base64
openssl enc -base64 -in rsawrappedkey.txt | tr -d '\n' | sed -e \ '$a\' > rsawrapencodedkey.txt
# View the RSA-wrapped key
cat rsawrapencodedkey.txt

# Format and mount the encrypted volume
sudo mkfs.ext4 /dev/disk/by-id/google-encrypted-disk-1 mkdir encrypted sudo mount /dev/disk/by-id/google-encrypted-disk-1 encrypted/
```
**Using custom keys for encryption**
```bash
# Enable cloudkms
> gcloud services enable cloudkms.googleapis.com
# Setup the name of key objects
> KEYRING_NAME=lab-keyring
> CRYPTOKEY_1_NAME=labkey-1
> CRYPTOKEY_2_NAME=labkey-2
# Create keyring
gcloud kms keyrings create $KEYRING_NAME --location us
# Create keys
gcloud kms keys create $CRYPTOKEY_1_NAME --location us \ --keyring $KEYRING_NAME --purpose encryption
gcloud kms keys create $CRYPTOKEY_2_NAME --location us \ --keyring $KEYRING_NAME --purpose encryption
# Obtain default encryption key information from a bucket
gsutil kms encryption gs://$DEVSHELL_PROJECT_ID-kms
# Assign Cloud KMS keys to a service account
# comand format is: gsutil kms authorize -p [PROJECT_STORING_OBJECTS] -k [KEY_RESOURCE]
gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME gsutil kms authorize -p $DEVSHELL_PROJECT_ID -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME
# set default key for a bucket 
gsutil kms encryption -k \ projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_1_NAME \ gs://$DEVSHELL_PROJECT_ID-kms

# encrypt individual objects
gsutil -o \ "GSUtil:encryption_key=projects/$DEVSHELL_PROJECT_ID/locations/us/keyRings\ /$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_2_NAME" \ cp file3.txt gs://$DEVSHELL_PROJECT_ID-kms
# Identify the key used to encrypt an object
gsutil ls -L gs://$DEVSHELL_PROJECT_ID-kms/file3.txt
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1NjgxMDIxNSwxNTQ5OTUyNTQzLDE1OD
I4ODc4NjIsMjEyODYwNTcxNiw0MjQxNjcyNjksLTM5MzQwNjQy
NywtMTM0OTI5NTAzMSwtMjAzMzU1ODI4MSw0NDI5OTUzNzMsLT
Q5MzUxOTIyMCwtOTY2NDYzMjExLDUxMjMxNzcxLDE1NTk4OTQz
MzUsNjUxNTU2Njc3XX0=
-->