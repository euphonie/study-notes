# Kubernetes Engine

- Authentication and authorization
	- User accounts can be accessed but not managed from kubernetes. They cannot be created or deleted from the command line using kubectl
		- These are normal users. Can be Google Account or Google Service Account.
		- Once created account types need to be authorized to create, read, update or delete Kubernetes resources
	- Service accounts are created and managed by Kubernetes, but only work within pods. 
	- Managed by Kubernetes API and bound to specific namespaces
- Requests without an account are anonymous
- Kubernetes Service Accounts are part of the clut


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwNzI5Njk2M119
-->