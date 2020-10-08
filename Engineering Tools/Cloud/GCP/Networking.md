
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
	- Managed by Google as a built-in feature
	- Restrict access to instances, incoming or outgoing
	- Defined through metadata tags on Compute Engine
		- VMs can be tagged (liked "web") and a firewall rule for incoming traffic on ports 80 and 443 can be assigned to all VMs with tag "web", **no matter what IP address it is**.
- Static routes creation for traffic forwarding
	- Through Routing Tables. Used to forward traffic between instances in the same network, even across subnets and between GCP zones, **with no need of external IP addresses**.
- SharingVPN content

**Objects** 
- Projects
	- Key organizer of infrastructure objects
	- Default quota of a project is 5 networks
	- Can be shared or peered with other projects
- Networks
	- Don't have IP addresses
	- Global 
	- Default
		-  defined in every project
		- one subnet per region with non-overlapping sider blocks
		- default firewall rules to allow ingress traffic from ICMP, RDP and SSH from anywhere, as ingress traffic from within the default network for all protocols and ports
	- Auto mode
		- default network
		- one subnet per region
		- regional IP allocation
		- Fixed /20 subnetwork per region
		- expandable up to /16
		- fit within 10.128.0.0/9 cider block
	- Custom mode
		- no default subnets created
		- Full control of IP ranges and subnets
		- regional IP allocation
		- Expandable to any RFC 1918 size
		- ranges cannot overlap between subnets of the same network
		- an auto mode network can be migrated to custom made for finer control
- Subnetworks. Allow to segregate environment
- Regions  and Zones. protection and high availability
- IP Addresses, provide internal and external use along with granular IP address range selection

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
- **Cloud VPN**
	- Traffic is encrypted by a VPN Gateway and decrypted by the receiving one.
		- Cloud VPN Gateway is inside GCP and provides an external IP address, the other Gateway, on-permise, is a physical, or virtual in case of other cloud provider, that also provides an external IP address
	- Useful for low volume data connections
		- Maximum transmission unit MTU = 1460 bytes, due to encryption and encapsulation
	- SLA 99.9%
	- Supports
		- Site-to-site vpn
		- static routes
		- dynamic routes (Cloud router). On-premise must have BGP enabled
		- IKEv1 and IKEv2 ciphers
	- VPNs can be used to connect with local infrastructure over the internet using the IPSEC protocol. It uses a **Cloud Router** that lets other networks and the VPC exchange route information over the VPN using the Border Gateway Protocol. 
		- For example having a subnet in VPC, the on-premise infrastructure automatically gets routes to it.
- **Peering** 
	- Not covered by a SLA
	- Direct Peering
		- For users that don't want to use the internet, for security concerns or reliability of the bandwidth, they can use Peering. Peering means putting a router in the same public data center as a Google point of presence and exchanging traffic. 
	- Carrier Peering
		- Peering through a contract with a partner that already has a PoP in Google's network
- **Dedicated InterConnect**
	- Covered by SLA
	- One or more direct private connections to Google 
	- Has higher uptime, up to 99.99% if the client's topologies meet Google's specifications
	- Can be backed up by a VPN for greater reliability

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzk5NDY5NDIsLTQ2OTUxMTAwNiw2OTk5Mj
YzNzIsLTQ2OTUxMTAwNiwtMzc0MDk5NjI2LC0xMzU3NDkxNTU5
LC0xNTY3NzE2MDI5LDE2MTIwMjI2MywxMTUyNzU2MTAwLDE3ND
kxOTU5MzEsLTQ3MDE4OTc3LDEyNTUwOTI5MjEsMTY1NDE2ODM3
OSwxMjgwMjQ4ODM5XX0=
-->