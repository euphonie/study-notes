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

```bash
# manual creation of signed URLs
gsutil signurl -d 10m ~/key.json gs://super-secure-bucket/noir.png
```

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

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4NzI4NzA2OSw0MjQxNjcyNjksLTM5Mz
QwNjQyNywtMTM0OTI5NTAzMSwtMjAzMzU1ODI4MSw0NDI5OTUz
NzMsLTQ5MzUxOTIyMCwtOTY2NDYzMjExLDUxMjMxNzcxLDE1NT
k4OTQzMzUsNjUxNTU2Njc3XX0=
-->