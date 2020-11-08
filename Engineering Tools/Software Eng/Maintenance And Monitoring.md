
# Maintenance and Monitoring

- Manage versions
	- Backwards compatibility, version in URI
	- Rolling updates allow to deploy new versions with no downtime
		- Feature of instance groups, just change the instance template
		- Default in kubernetes, just change the image
		- Automated in App Engine
	- Blue/green deployments
		- Blue is current version, green is a new version
		- Once green is tested migrate requests to it
		- If failure occurs switch back
		- In CE use DNS to migrate requests from one load balancer to another
		- Kubernetes, configure service to ro

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDc0NjUyODddfQ==
-->