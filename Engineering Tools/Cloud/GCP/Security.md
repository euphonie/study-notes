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
- Window instances accessed via Remote Desktop Protocol
	- Require username and password
- Connecting from outside Google Console
	- Is possible with a username and valid SSH key
		- Key needs to be provided to the instance using the project's metadata `SSH Keys` tab

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjY3ODI2OTc5XX0=
-->