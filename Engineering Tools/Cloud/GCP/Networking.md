
# Networking

A subnet corresponds to a set of IP addresses or segment. 

- Each VPC network is contained in a GCP project, a default VPC, and belongs to this project.
- VPC has global scope and subnets have regional scope.
- It has global scope and can have subnets spanning different zones worldwide.

Is arranged around VPC networks. Topics like:
- External IP 
- Network segmentation
- Firewall rules
	- Global distributed firewall already provided
	- Restrict access to instances, incoming or outgoing
	- Defined through metadata tags on Compute Engine
		- VMs can be tagged (liked "web") and a firewall rule for incoming traffic on ports 80 and 443 can be assigned to all VMs with tag "web", **no matter what IP address it is**.
- Static routes creation for traffic forwarding
	- Through Routing Tables. Used to forward traffic between instances in the same network, even across subnets and between GCP zones, **with no need of external IP addresses**.
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


## Peering

Communication between VPCs can be established, so they can exchange traffic, through VPC Peering. Using Shared VPCs the user can share networks or individual subnets with other GCP projects


## Cloud Load Balancing

Fully distributed and software-defined managed service for all the traffic. They run apart from VMs, so there's no worry for scaling or management.
- Users get single, global anycast IP address
- Works in front of HTTP, HTTPS, TCP and UDP traffic
- Works cross-region
	- Regional
		- Any traffic (UDP, TCP), supported on any port number
	- Regional Internal
		- Traffic inside VPC, used for internal tiers of multi-tier applications
	- Regional options
		- Global HTTP(S). Based on load, can route diff URLs to diff backends
		- Global SSL Proxy. non-HTTPS SSL traffic supported on specific ports
		- Global TCP Proxy. non-SSL TCP traffic, supported on specific ports
- Automatic multi-region failover
- Reacts to changes based in
	- users, traffic, backend health, network conditions and others
- No pre-warnings for pikes in traffic

## Cloud DNS

Create managed zones, then add, edit, delete DNS records. DNS translates internet host names to addresses.
- It has low latency and high-availability
- It's programmable through Console, a RESTful API or command line

## Cloud CDN

Google has edge caches that can distribute content that is closer to users.
- Lower network latency
- Reduced load at the origin of the content to reduce costs

## Hybrid Connectivity

Users want to use their already established services along with VPC in GCP. 
- VPN
	- VPNs can be used to connect with local infrastructure over the internet using the IPSEC protocol. It uses a **Cloud Router** that lets other networks and the VPC exchange route information ove

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTczMjQxNCwxNjEyMDIyNjMsMTE1Mj
c1NjEwMCwxNzQ5MTk1OTMxLC00NzAxODk3NywxMjU1MDkyOTIx
LDE2NTQxNjgzNzksMTI4MDI0ODgzOV19
-->