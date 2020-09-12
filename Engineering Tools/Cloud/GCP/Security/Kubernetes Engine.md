# Kubernetes Engine

- Authentication and authorization
	- User accounts can be accessed but not managed from kubernetes. They cannot be created or deleted from the command line using kubectl
		- These are normal users. Can be Google Account or Google Service Account.
		- Once created account types need to be authorized to create, read, update or delete Kubernetes resources
	- Service accounts are created and managed by Kubernetes, but only work within pods. 
	- Managed by Kubernetes API and bound to specific namespaces
- Requests without an account are anonymous
- Kubernetes Service Accounts are part of the cluster in which they are defined and are used only in the cluster.
	- In contrast, Google Service Accounts are part of a GC project and can be granted permissions to clusters and other Cloud resources
- Google Service Accounts should not be used in Kubernetes, only when their extra capabilities are really needed and use Cloud IAM to manage permissions
- RBAC can be used for finer access to resources

**Hardening Clusters**
- Upgrade GKE infrastructure in a timely fashion
	- Masters are patched and updated automatically
	- Node auto-upgrade, can be disabled but recommended to manually update monthly or another set schedule
- Monitor cluster configurations
	- Security health analytics can be enabled to alert for any anomalies
- Restrict access to planes and nodes
	- By default the GKE cluster has internet routable IP addresses that can be accessed from any IP address
	- A private cluster can also be selected from creation
	- Options
		- **Public endpoint access disabled**. Prevents all internet access for masters and nodes. Works with networks using Cloud Interconnect and Cloud VPN.
		- **Public endpoint access enabled, master authorized networks enabled**. Gives the control plane a public IP address. Installs a custom firewall rule base.
		- **Public endpoint access enabled, master authorized networks disabled**. Default setting, allows all public internet users to make connections to the control plane.
			- To disable direct internet access to nodes, specify the G Cloud tool option, enable private nodes and cluster creation.
- Consider using Group Authentication
	- Security best practice
	- Google groups for GKE must be enabled when creating the clusters
- Shielded GKE nodes provide verifiable node identity and integrity
	- Upon cluster creation or uptake, specify the GCloud option, enabled shielded nodes. 
- Restricting network access between nodes in the same network reduces lateral mobility for attackers and provides protection against accidental or deliberate denial-of-service
	- To restrict access use Istio, which offers load balancing, service authorization, throttling, quota and metrics
	- Or use Kubernetes network policies to provide basic access control functionality
- Secret management for authenticated secrets.
	- These are generally stored in the etc.d directory
	- A third-party secret manager should be configured, such as HashiCorp Valut, which can be integrated with GKE clusters and should be set up before.
	- Another option, is to use Kubernetes secrets natively, making sure to encrypt the application layer with a key that you manage
- Enabled Workload Identity to remove th eneed to use node service accounts or to export service account keys into secrets.
	- Enabled enforcement of the principle of least privilege, and lets manage namespace service account credentials, lowering the risk of exposure, and reduces the burden of manually rotating those credentials
- Create and use a service account with a minimal privilege to run you GKE cluster instead of the default compute engine service account
	- GKE requires at minimum the roles
		- monitoring.viewer
		- monitoring.metricwriter
		- logging.logwriter
- Harden against discovery exploits
	- Configure authorized networks to restrict access to only a set of IP ranges
	- Setup a private cluster to restrict access to only certain VPCs
	- Correct the subjects of the default system discovery and system basic user cluster role bindings
	- Allow access by only certain known users and groups

**Securing Workloads**

- Limit pod container process privileges
	- GKE allow t oset security-related options via the security context on both pods and containers. Ex. change the run as user and group.
- Use workload Identity
	- The pods running GKE can have the permissions assigned to a Google Service Account 
- Enable Binary Authorization

**Monitoring and Logging**
- Kubernetes engine monitoring is enabled by defult and provides a monitoring dashboard tailored for k8s.
	- Control if it collects application logs
	- And disable cloud monitoring or logging completely
- In the dashboard
	- Key performance metrics. CPU utilization, memory utilization and the number of open incidents
	- Hierarchies. 
		- Infrastructure organizes resources by cluster, then node, then pod and then by container.
		- Workload organizes resources by cluster, then namespace, then workload, then pod and lastly by container.
		- Services by cluster, namespace, service,


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1NDcyMzk5OSwxNzk2ODgwMjY5LDI0MT
QwMjEwXX0=
-->