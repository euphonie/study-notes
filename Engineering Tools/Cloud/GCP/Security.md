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

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc5NDUyMTE4Ml19
-->