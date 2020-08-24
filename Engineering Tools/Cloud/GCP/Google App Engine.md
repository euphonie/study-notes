
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
	- **Flexible**
		- If any restrictions from the standard model don't work
		- Application runs inside a Docker container on Compute Engine's VMs
		- User chooses the geographical region to run
		- VMs managed by Google
		- Can access Google services
			- data store, memcached, task queues, etc.
		- startup in minutes
		- ssh access, not by default
		- write to disk but ephemeral
		- support for 3rd party binaries
		- network access
		- Pay for resource allocation per hour, no automatic shutdown
- Automatically scales app in response to the traffic
- Provides
	- No-SQL databases
	- In-Memory caching
	- Load Balancing
	- Health Checks
	- Logging
	- Authentication


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM2NTA2OTc5XX0=
-->