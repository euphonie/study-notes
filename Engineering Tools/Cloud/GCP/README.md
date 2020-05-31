# About




## Instance templates

Provision multiple instances at the same time

## Identity & Access Management


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
eyJoaXN0b3J5IjpbMTE3MDc1MjU4MywtNTQ0MjQ3MTU1LC04NT
E1MTM2NDksNzQ1Mzk4NjgwXX0=
-->