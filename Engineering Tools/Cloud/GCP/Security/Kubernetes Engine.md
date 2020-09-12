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


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwOTgxMzc4Ml19
-->