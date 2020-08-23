
# Google App Engine

Platform as a Service.
App Engine manages the hardware and networking infrastructure required to run code.
- Easy deployment, maintenance and scalability
- Suited for applications where the workload is highly variable or unpredictable, web applications and mobile backends
- Two environments
	- **Standard**. Simpler experience and fine-grained auto-scale
		- Free daily quota for some services
		- SDK for main languages and test locally and deploy
		- Might be free for applications that need few resources
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
		- support for 3rd party 
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
eyJoaXN0b3J5IjpbMjY3ODIzMzg0LDE1NDEyOTYxMjcsLTc1MT
c5ODA0MSwxNDk2MTczMDc4LDY5MTE1ODMyXX0=
-->