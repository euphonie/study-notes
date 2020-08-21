
# Networking

A subnet corresponds to a set of IP addresses or segment. 

- Each VPC network is contained in a GCP project, a default VPC.
- VPC has global scope and subnets have regional scope.
- It has global scope and can have subnets spanning different zones worldwide.

Is arranged around VPC networks. Topics like:
- External IP 
- Network segmentation
- Firewall rules
- Static routes creation for traffic forwarding
	- Through Routing Tables. Used to forward traffic between instances in the same network, even across subnets.
- SharingVPN content

The size of a subnet in a custom network can be increased by expanding the range of IP addresses allocated to it. And it doesn't affect already configured VMs.

VMs can be allocated on different regions but still belong to the same subnet inside a VPC, and share continuous IP segments. 

## Services
- Load balancers
	- Global Load balancers
	- Regional Load balancer
- Cloud DNS
- Cloud CDN
	- Global distribution of content
- Hybrid connectivity
	- Link on-premise data centers to Google Cloud


## Load Balancing



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NjQ2ODA1OTUsMTY1NDE2ODM3OSwxMj
gwMjQ4ODM5XX0=
-->