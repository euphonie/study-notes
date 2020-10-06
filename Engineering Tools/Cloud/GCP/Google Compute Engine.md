
# Google Compute Engine

Let's you create and run VMs inside Google's infrastructure.
- No upfront investment
- Can run thousands of virtual CPUs
- Instances can be created from
	- Google Cloud Platform console
	- GCloud command line tool
- Can run linux or windows images, by Google, custom versions or imported from physical servers
- Most control
- Predefined Custom Machine Types
	- Max 128 Persistent disks
	- High-memory memory intensive tasks
	- High-cpu machine types
	- Memory-optimized machine types
		- In-memory databases
		- business warehouse workloads
		- Genomic analysis
		- SQL Analysis Services
	- Compute-optimized machine types
	- Shared-core machine types
		- Small non-resource intensive computations
		- f1-micro, g1-small
- Use community images or own
- Patch software
- Auto scaling can be configured based on traffic volume in specific regions
- Run third-party software, attach GPU and TensorFlow Processing Unit (TPU)
- Lift-and-shift migration for migrating VMs completely
- Micro VMs share a CPU with other virtual machines.

By choosing a machine type it assigns. Custom machine types can also be created
- Number of Virtual CPUs (Max: 96)
- Memory (Max in beta: 624 GB)
- GPUs (available in many GCP zones)
- Persistent Storage
	- Standard. Default
	- SSD
		- There's an option of using local SSD storage for scratch space but it's volatile and it's removed when the VM terminates.
			- Scratch space is space on a disk dedicated to temporary user data
- Boot Image (Linux or Windows)
- Startup scripts for dependencies installation and environment setup

Snapshots can be applied to running VMs. These can be kept as backups or use them when migrating to another region.

**Choosing VM specs**
- Computation
	- Network throughput scales 2 Gbps per vCPU 
	- Theoretical max of 32 Gbps with 16 vCPU or 100 Gbps with T4 or V100 GPUs
	- A vCPU is equal to 1 hardware hyper-thread
- Disk
	- Performance vs cost.
	- SSDs higher number of IOPS per dollar
		- Local SSDs have higher IOPS but are volatile, working only for the assigned instance session. Should be used as a swap disk
	- Standard disks higher amount of capacity per dollar

**VMs access**
- Linux, SSH using tcp:22
- Windows, RDP using tcp:3389
- VM Lifecycle
	- Provisioning
		- Virtual CPUs, Memory
		- Root disk, persistent disk
		- Additional disks
	- Staging
		- Ip addresses internal external
		- System image from Cloud storage
		- Boot
	- Running
		- Startup script
		- Access SSH/RDP
	- Export system image, set/get metadata, snapshot persistent disk, move VM to different zone
	- Stopping
		- Shutdown script
	- Terminated
		- Not charged for VM but for attached disks and reserved IPs
		- Delete, restart, availability policty

## Preemptible VMs

The only difference is that Compute Engine has the permission to terminate the VM if it's resources are needed elsewhere.
- Per-second billing, sustained use discounts
- High throughput to storage w/o extra cost
- Custom machine types: only pay for needed hardware
- **Note** the job needs to be able to be stopped and restarted

## Auto scaling

- Big VMs are good for workloads like in-memory databases and CPU intensive analytics
- Scaling out is usually most used instead of scaling up
- Auto scaling lets the user add and take away VMs from your application based on load metrics. Another alternative is using VPC's load balancing.

# Best Practices 

- Control access to resources with projects and IAM roles
- Isolate machines using multiple networks. Implement VPC networking
	- If projects don't require network communication amongst them, host them in different networks
- On hybrid-setups, use VPN or Cloud Interconnect to securely connect to GCP
- Use Cloud Audit Log to generate logs for API operations in CE
- Only allow VMs to be created from approved images 
	- Only ones that contain approved software that meets your policy or security requirements
	- Use the Trusted Images Policy
- Harden custom OS images to help reduce the surface of vulnerability for the instance
	- Formulate a plan to maintain the image with security patches and updates
- Deployed Compute Engine instances are not updated automatically
	- The image should be patched and each instance should be replaced with an updated image
- Each instance that needs to call a Google API should run as a service account with the minimum permissions necessary for that instance to do its job
	- Create a new service account rather than using the default
	- Run IAM roles to that service account for only the resources needed
	- Configure the instance to run as that service account


# Snippets 

```bash
# Create VM using gcloud
gcloud compute instances create [instance-name]
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MzIzODE2MjgsLTE0NDc2OTk0MSwtND
UyOTI1ODYxLDExMzQxMzE2MiwtNDU3MjAxOTc0LC0xNzIzODc1
ODQ1LDMyMTk0ODc2NiwtMjEyNTEyOTE3XX0=
-->