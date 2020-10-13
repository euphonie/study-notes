
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
	- per second charges after a one-minute minimum
	- Google, premium images
	- Linux 
	- Windows
		- charged per minute after 10-minute minimum
	- Custom images
		- import on-prem, workstation or another cloud
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

**Disk options**
- Boot disk
	- Every VM comes with a single root persistent disk
	- Image is loaded during first boot
		- Bootable: attach to a VM and boot
		- Durable: survives VM termination
	- Some OS images are customized for CE
	- Disable "Delete boot disk when instance is deleted" to keep 
- Persistent disk
	- Local SSD disks
		- They are physically attached to a VM
		- Ephemeral
		- More IOPS, lower latency, higher throughput
		- 375 GB disk up to 8, total 3TB
		- Data survives reset but not VM stop/termination
		- Cannot be reattached to a different VM
		- Best option
			- Even higher performance, but no redundancy
	- HDD or SDD
	- Disk resizing
	- Attached to read-only mode to multiple VMs
	- Attached to VM through network interface
	- Durable storage
	- Bootable
	- Incremental snapshots
	- Performance scales with size 
	- Best option
		- HDD. Don't need performance  just capacity
		- SDD. High-performance, provides data redundancy
- RAM disk
	- tmpfs can be used to strore data in memory
	- Faster than local disk, slower than memory
		- Use when app expects file system structure and cannot directly store data in memory
		- Fast scratch disk or fast cache
	- Very volatile, erase on stop/restart
	- Persistent disks can be used to back up RAM disk data
	- Best option
		- Highest performance, but volatile

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

## Moving an instance to a new zone

- Within region
	- gcloud compute instances move
	- Update references to VM; not automatic
- Between regions
	- Snapshot all persistent disks on the source VM
	- Create new persistent disks in destination zone restored from snapshots
	- Create new VM in the destination zone and attach new persistent disks
	- Assign static IP to new VM
	- Update references to VM
	- Delete the snapshots original disks and original VM

## Snapshots
- Not available for local SSD
- Creates an incremental backup to Cloud Storage
	- Not visible in buckets
	- Consider cron jobs for periodic incremental backup
- Snapshots can be restored to a new persistent disk
	- Can be in another region or zone
	- Snapshot doesn't back up VM metadata, tags, etc.
- Can be used to
	- move between regions
	- move to a different zone
	- transfer from HDD to SSD to improve performance
	- Resize persistent disk to improve storage capacity. Disks can grow but not shrink.

## Managed instance groups
- Deploy identical instances based on instance template
- Instance group can be resized
- Manager ensures all instances are runnning
	- Automatically recreates failing instances, uses same name and template from previous instance
- Typically used with autoscaler
	- Can automatically scale all instances
- can be single zone or regional
	- Regional are recommended, spreads app load to multiple zones
	- Protects against zonal failures
- To create
	- First create an instance template
	- Create a managed instance group of end specific instances
	- Instance group manager populates the group based on the instance template

**Autoscaling**
- Automatically add or remove instances based on load
- Define autoscaling policy based on measure
	- CPU utilization
	- Load balancing capacity
	- Monitoring metrics
	- Queue-based workload


## Preemptible VMs

The only difference is that Compute Engine has the permission to terminate the VM if it's resources are needed elsewhere.
- Per-second billing, sustained use discounts
- High throughput to storage w/o extra cost
- Custom machine types: only pay for needed hardware
- might be terminated at any time
	- 24 hours max
	- No charge if terminated in the first 10 minutes
	- 30 second terminate warning, but not guaranteed
- no live migrate; no auto restart
- **Note** the job needs to be able to be stopped and restarted

## Sole-tenant nodes
- Physical CE server that is dedicated to hosting VM instances only for your specific project
- Workloads that require physical isolation from other workloads or VM in order to meet compliance requirements
- Like having a payment processing workload that needs to be isolated from other processes
- All instances belong to the same project
- The user can use own license

## Shielded VMs

Refer to Security > Compute Engine

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

```bash
#mounting a disk in a VM
# Create directory that serves as the mount point
sudo mkdir -p /home/minecraft
# Format the disk 
sudo mkfs.ext4 -F -E lazy_itable_init=0,\ lazy_journal_init=0,discard \ /dev/disk/by-id/google-minecraft-disk
# Mount the disk
sudo mount -o discard,defaults /dev/disk/by-id/google-minecraft-disk /home/minecraft
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE1NjgyODMwLC02Njk4Mjg2MDAsODEwNj
kwNTczLDEwODI0NTk5ODksLTM0NDYxNDQ3OSwtMTQzMjM4MTYy
OCwtMTQ0NzY5OTQxLC00NTI5MjU4NjEsMTEzNDEzMTYyLC00NT
cyMDE5NzQsLTE3MjM4NzU4NDUsMzIxOTQ4NzY2LC0yMTI1MTI5
MTddfQ==
-->