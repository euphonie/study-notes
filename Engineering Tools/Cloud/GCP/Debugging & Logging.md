
# Debugging and Logging

## Stackdriver
- Combines metrics logs and metadata
- Gathers from GCP, AWS, on premise or hybrid cloud
- Single comprehensive view and take action
- Features
	- Logging
	- Monitoring
	- Error Reporting
	- Stackdriver APM 
		- Identify bottlenecks and find resolution
		- Understand how applications behave in production
		- Tools used in Google SRE (Service Reliability Engineering)
		- Tools
			- Trace
				- Analyzes traces and provides reports of application degradations
				- Inspect latency for single request or aggregated
				- Find bottleneck 
				- Find root cause
				- Automatically identifies recent changes
				- Versions of reports to be compare through time
				- Works on multiple VMs doesn't matter the provider
			- Debugger
			- Profiler 
				- Uses statistical techniques and low impact instrumentation to provide performance without affecting the app
				- Helps identify potential performance issues
- Increases reliability
- Identify trends and prevent issues
- Reduce monitoring overhead

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUwMzU4OTExMSwtMzkzMjM4NTk1XX0=
-->