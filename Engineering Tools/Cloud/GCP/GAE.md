
# Google App Engine

Platform as a Service.
App Engine manages the hardware and networking infrastructure required to run code.
- Easy deployment, maintenance and scalability
- Suited for applications where the workload is highly variable or unpredictable, web applications and mobile backends
- Two environments
	- Standard. Simpler experience and fine-grained auto-scale
		- Free daily quota for some services
		- SDK for main languages and test locally and deploy
		- App runs in a runtime. Only in Java, Python, PHP and Go
			- Include libraries that support App Engine APIs
		- Applies restrictions through a sandbox
			- No writing to local files
			- All requests time out at 60s
			- Limits on third-party software
	- Flexible
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
eyJoaXN0b3J5IjpbODU4NjM3NDkyLC03NTE3OTgwNDEsMTQ5Nj
E3MzA3OCw2OTExNTgzMl19
-->