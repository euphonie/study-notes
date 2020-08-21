
# Google Compute Engine

Let's you create and run VMs inside Google's infrastructure.
- No upfront investment
- Can run thousands of virtual CPUs
- Instances can be created from
	- Google Cloud Platform console
	- GCloud command line tool
- Can run linux or windows images, by Google, custom versions or imported from physical servers

By choosing a machine type it assigns. Custom machine types can also be created
- Number of Virtual CPUs
- Memory
- GPUs (available in many GCP zones)
- Persistent Storage
	- Standard. Default
	- SSD
		- There's an option of using local SSD storage for scratch space but it's volatile and it's removed when the VM terminates.
			- Scratch space is space on a disk dedicated to temporary user data
- Boot Image (Linux or Windows)
- Startup scripts for dependencies installation and environment setup

Snapshots can be applied to running VMs. These can be kept as backups or use them when migrating to another region.

## Preemptible VMs

The only difference is that Compute Engine has the  permission to terminate the VM if it's resources are needed elsewhere.
- Per-second billing, sustained use discounts
- High throughput to storage w/o extra cost
- Custom machine types: only pay for needed hardware

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzMTE0MDY5OV19
-->