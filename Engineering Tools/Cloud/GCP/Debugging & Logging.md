
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
					- Overall latency
					- Latency through time
					- Application Latency dependencies
				- Find bottleneck 
				- Find root cause
				- Automatically identifies recent changes
				- Versions of reports to be compare through time
				- Works on multiple VMs doesn't matter the provider
				- Zipkin collector available
			- Debugger
				- Collects debug snapshots
				- Inject logging information without interfering the application
			- Profiler 
				- Monitor CPU and heap
				- Identifies inefficiently writing code or poorly performing code
				- Analyzes memory intensive functions
				- Works in multiple cloud providers or hybrid setup
				- Needs to install a profiling agent
				- Creates a profile by collecting 10 seconds of data every 1 minute
				- Uses statistical techniques and low impact instrumentation to provide performance without affecting the app
				- Helps identify potential performance issues
- Increases reliability
- Identify trends and prevent issues
- Reduce monitoring overhead

```bash
# Install debug agent
npm install --save @google-cloud/debug-agent
# Produce a source context file (Creates source-context.json to display the correct source code in GCP Debug window)
gcloud debug source gen-repo-info-file --output-directory .

# Install error reporting
npm install --save @google-cloud/error-reporting
```

```javascript
// import debug-agent
allowExpressions Boolean property set to true. require('@google-cloud/debug-agent').start({ allowExpressions:  true  });
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0OTY4MTY3Myw2MzU4MTcxMjMsMTg5ND
k4MDI4OCwtMzkzMjM4NTk1XX0=
-->