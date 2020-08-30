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


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTEyMzE3NzEsMTU1OTg5NDMzNSw2NTE1NT
Y2NzddfQ==
-->