
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
- Shared VPCs
	- Centralized network administration
	- Only works within same organization
	- When you share a VPC, you designate a project as a host project, and attach one or more other service projects to it.
- VPC peering
	- Across organizations and within a project; decentralized
	- VPC peering is a descentralized or distributed approach to multiproject networking
		- each VPC network may remain under the control of separate administrator groups, and maintains its own global firewall and routing tables
		- Don't incur in network latency, security and cost drawbacks present when using external IP addresses or VPNs

## Cloud Load Balancing

Fully distributed and software-defined managed service for all the traffic. They run apart from VMs, so there's no worry for scaling or management.
- Users get single, global anycast IP address
- Works in front of HTTP, HTTPS, TCP and UDP traffic
- Works cross-region
	- Regional
		- Any traffic (UDP, TCP), supported on any port number
	- Regional Internal
		- Traffic inside VPC, used for internal tiers of multi-tier applications
		- Internal HTTP(S)
		- Internal TCP/UDP
			- Andromeda
		- Network TCP/UDP
			- Maglev. Distributed software system
	- Global options
		- Global HTTP(S). Based on load, can route diff URLs to diff backends
		- Global SSL Proxy. non-HTTPS SSL traffic supported on specific ports
		- Global TCP Proxy. non-SSL TCP traffic, supported on specific ports
- Automatic multi-region failover
- Reacts to changes based in
	- users, traffic, backend health, network conditions and others
- No pre-warnings for pikes in traffic

**Balancing**
- HTTP(S) Load balancing
	- Global load balancing
	- anycast IP Address
	- HTTP multiple regions
	- HTTP: 80, 8080; HTTPS: 443
	- IPv4, IPv6
	- Autoscaling and no pre-warming
	- URL maps
	- Requests are routed to the closest instanced group to the user
	- Arch
		- Internet > Global Forwarding Rule > Target Proxy > URL Map > Backend Service > Instance groups
	- Backend Services
		- Health check to know if it should route request
		- Session affinity to keep communication between same client and service
		- Round-robin assignment
		- Time out setting (30 sec)
		- 

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
	- Capacity of 1.5-3Gbps per tunnel, traffic through public internet
		- Multiple tunnels can be configured
	- Supports
		- Site-to-site vpn
		- static routes
		- dynamic routes (Cloud router). On-premise must have BGP enabled
		- IKEv1 and IKEv2 ciphers
	- VPNs can be used to connect with local infrastructure over the internet using the IPSEC protocol. It uses a **Cloud Router** that lets other networks and the VPC exchange route information over the VPN using the Border Gateway Protocol. 
		- For example having a subnet in VPC, the on-premise infrastructure automatically gets routes to it.
- **Peering** 
	- Layer 3 connections
	- Not covered by a SLA
	- Provide access to public IP addresses
	- Useful when access is required to Google and Google Cloud properties.
	- Done by exchanging BGP routes between Google and the peering entity
	- Direct Peering
		- 10 Gbps per link
		- For users that don't want to use the internet, for security concerns or reliability of the bandwidth, they can use Peering. Peering means putting a router in the same public data center as a Google point of presence and exchanging traffic. 
		- Directly to Google
	- Carrier Peering
		- Capacity varies based on partner offering
		- Peering through a contract with a partner that already has a PoP in Google's network
		- 	Shared through a partner
- **Dedicated InterConnect**
	- Layer 2 connection
	- Covered by SLA
	- Capacity of 10 Gbps per link 
		- Multiple links can be configured
	- Transfer large amounts of data between networks
	- One or more direct private connections to Google 
	- Has higher uptime, up to 99.99% if the client's topologies meet Google's specifications
	- Directly to Google
	- Can be backed up by a VPN for greater reliability
	- Uses VLAN, connection to internal IP addresses RFC 1918
	- It needs to provision a cross-connect between the Google network and your own router in a common co-location facility
	- To exchange routes you configure a BGP session over the CloudRouter and the on-premise router
		- Allows user traffic from on-premise network to reach GCP resources on the VPC network and viceversa
- **Partner InterConnect**
	- Layer 2 Connection
	- Capacity of 50 Mbps - 10Gbps per connection
	- Shared through a partner
	- 99.9 or 99.99 SLA between Google and Service Provider
	- Uses VLAN, connection to internal IP addresses RFC 1918
	- Need to consider when your own-premise infrastructure is not near of one o the co-location facilities. 
		- Or if data needs don't warrant a Dedicated Interconnect
	- To exchange routes you configure a BGP session over the CloudRouter and the on-premise router
		- Allows user traffic from on-premise network to reach GCP resources on the VPC network and viceversa

# Choosing a Connection Type

![How to choose a connection](https://raw.githubusercontent.com/euphonie/study-notes/master/Engineering%20Tools/Cloud/GCP/choosingConnection.png)

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODAyNjcyNTYwLDExNzUxNDcyNiw0NTAzND
gzMDEsMTg3MDE2MzE2OSwtMTkwNjkyNzU0LC0xNDY3NjgwOTU4
LDE1NDU5NDkyNzYsMjg1MzYzMzg2LDM5OTQ2OTQyLC00Njk1MT
EwMDYsNjk5OTI2MzcyLC00Njk1MTEwMDYsLTM3NDA5OTYyNiwt
MTM1NzQ5MTU1OSwtMTU2NzcxNjAyOSwxNjEyMDIyNjMsMTE1Mj
c1NjEwMCwxNzQ5MTk1OTMxLC00NzAxODk3NywxMjU1MDkyOTIx
XX0=
-->