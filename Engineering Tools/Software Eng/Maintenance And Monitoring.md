
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
		- Kubernetes, configure service to route to the new pods using labels
		- App Engine, use the Traffic Splitting feature
	- Canary releases
		- Current service version continues to run
		- Deploy an instance of the new version and give it a percentage of requests
		- Monitor for errors
		- Compute Engine, create a new instance group and add it as an additional backend in your load balancer
		- Kubernetes, create new pod with same labels the service will automatically route a portion of requests to it
		- App Engine, use Traffic Splitting


## Cost Planning 

- Capacity Planning
	- Forecast. Estimate capacity needed, monitor, repeat
	- Allocate. Determine resources required to meet forecasted capacity
	- Approve. Cost estimation versus risks and rewards
	- Deploy. Monitor to see how accurate your forecasts were

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODEyMzE1MTldfQ==
-->