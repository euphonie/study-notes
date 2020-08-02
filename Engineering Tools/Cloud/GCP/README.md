# Google Cloud Platform

## Instance templates

Provision multiple instances at the same time

## Identity & Access Management

Google cloud is organized through the concept of projects. An organization can have multiple projects and within those projects folders and individual resources can be contained. Rules and permissions can be assigned to any element in this hierarchy. 
- Folders can be used to assign policies, as all the resources in a folder inherit the IAM policies from the folder.

### Organization

## Network Services

### Load balancers (internal or external)

External load balancers might be used for connections between clients and app servers, and internal load balancers might be used within app servers to connect web tiers with database tiers.

- HTTP(S) load balancer
	- Provides global, any instance
- Network load balancer
	- Balances regional TCP and UDP traffic

### Configuration in GCP

- A load balancer can be assigned to an instance group. The instance group is assigned as the backend service.
- A balancing mode of utilization is recommended in a high transaction rate.
- Load balancer can use a Health check to determine where to route the requests.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDM5MTQxNzgxLDExNzA3NTI1ODMsLTU0ND
I0NzE1NSwtODUxNTEzNjQ5LDc0NTM5ODY4MF19
-->