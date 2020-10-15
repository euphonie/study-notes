
# Google App Engine

![Standard workflow](https://raw.githubusercontent.com/euphonie/study-notes/master/Engineering%20Tools/Cloud/GCP/appengine.png)

Platform as a Service.
App Engine manages the hardware and networking infrastructure required to run code.
- Easy deployment, maintenance and scalability
- Suited for applications where the workload is highly variable or unpredictable, web applications and mobile backends
- Two environments
	- **Standard**. Simpler experience and fine-grained auto-scale
		- Free daily quota for some services
		- SDK for main languages and test locally and deploy
		- Might be free for applications that need few resources. After free daily quota pay per instance class, with automatic shutdown.
		- App runs in a runtime. Only in Java, Python, PHP and Go
			- Include libraries that support App Engine APIs
		- Applies restrictions through a sandbox
			- No writing to local files
			- All requests time out at 60s
			- Limits on third-party software
			- startups in milliseconds
		- Good for spiky or variably traffic
		- Standard APIs only work in GAE Standard environments
	- **Flexible**
		- If any restrictions from the standard model don't work
		- Default settings for infrastructure components
		- Application runs inside a Docker container on Compute Engine's VMs
			- container can run on GKE
		- User chooses the geographical region to run
		- custom healthchecks
		- VMs managed by Google
		- Can access Google services
			- data store, memcached, task queues, etc.
		- startup in minutes
		- ssh access, not by default
		- write to disk but ephemeral
		- support for 3rd party binaries
		- network access
		- Pay for resource allocation per hour, no automatic shutdown
		- Behind the scenes App engine provisions
			- Load balancer
			- Deploys the application in three different zones
			- Launches autoscale CE instances 
			- Sets up Monitoring, Logging, Error Reporting, Health check and SSL
		- Applies automatic updates to the containers
		- Enables to perform canary testing or A/B testing by splitting traffic
		- Can work with Jenkins/Spinnaker
		- Consider other solution if 
			- App with protocol != {HTTP/S}
			- Persistent disks are needed
			- Spiky or very low traffic, there are always two instances running
- Automatically scales app in response to the traffic
	- In app.yaml configuration options can be used
		- Target_cpu_utilization
		- Target_throughput_utilization
		- Max_concurrent_requests
		- Max_pending_latency
		- Min_pending_latency
- Provides
	- No-SQL databases
	- In-Memory caching
	- Load Balancing
	- Health Checks
	- Logging
	- Authentication

## Traffic Splitting
- 3 ways to split traffic
	- IP address
		- stickiness so all traffic from IP address are handled by some instances, if user
	- HTTP cookie
	- Random selection

# Scripts

```bash
# Deploy app to flexible environment using a .yaml file
gcloud app deploy ./frontend/app.yaml
# Check all components are up to date in Command Console
gcloud components install app-engine-python
```
**app.yaml**
```yaml
runtime: nodejs
environment: flex
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTU1OTUyNjEsMTAxODQ2OTIwLC0xMD
g1NzYzMjY0LDEzNjUwNjk3OV19
-->