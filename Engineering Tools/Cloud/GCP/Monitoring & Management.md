# Monitoring & Management

Reliable release process involves release and testing phases of software delivery. Main components for CI/CD pipelines.

**CI Pipeline**
- Pull from master
- Commit to feature branch
- Push to repository
	- Cloud Source
	- Github
- Build triggers in Jenkins, Circle CI, Github Actions, etc.
- Create image and store in artifact repository like Container registry
- Deployment manager like Spinnaker deploys the image
- Run test suites 
- If test are successful code can be promoted to a release branch

**CD Pipeline**
- It involves no manual stages
- The deployment system deploys the application images to the staging environment
- Runs integration tests, performance tests and more
- If tests are successful the image is tagged as a release candidate
- Approval of release candidate can trigger deployment to canary or blue-green production environments
- Monitor the performance of production using services like StackDriver
- If deployment works successfully entire traffic can be switched to the new release
- If there are any errors a rollback to the last stable release can be performed

##  Cloud Build
- Fully managed service
- Set up build pipelines to create a Docker container image and push the image to a Google Cloud resource
- Pipeline is automatically triggered by changes to the repository
	- Push to a branch, push of a tag, etc.
- Requires a build configuration file that specifies the steps of the pipeline
- Each step is a docker container executing the script indicated
	- Step name identifies the container image
	- Image attribute identifies the base image for the container
- Can be specified in YAML or JSON notation
- Source code is mounted to the /workspace directory
	- The artifacts are persisted in the directory
- Publishes build status notifications to Cloud Pub/Sub
- 

## Container Registry
- Registry for images uploaded to Google Cloud


# Performance checkpoints

- In Development
	- Check performance watchpoints related to incoming requests
		- Web authoring
			- Web page design and implementation
			- Pagespeed insights
				- Lack of caching headers
				- Lack of compression
				- Too many HTTP browser requests
				- Slow DNS response 
				- Lack of minification
			- Chrome dev tools
		- Cold-boot performance
			- Operations during initial boot of VM
		- Self-inflicted load
			- Service-to-service or browser-to-service calls
			- Polling cron jobs, 
			- batch requests
			- multiple ajax requests
			- Chrome devtools
			- sever side load analysis
			- Stackdriver Trace
	- Review application code and logs
		- Application errors
			- HTTP errors and other exceptions
		- Runtime code Gen
			- Aspect-oriented programming
		- Static resources
			- Static web pages, images
			- Use a CDN with Cloud Cloud Storage
		- Caching
			- Database retrieval and computation
			- Cache HTML-generated fragments
		- One-at-a-time Retrieval
			- Multiple serial requests
		- Error-Handling
			- Exponential backoff
			- Implement circuit-breaker after certain amount of errors
			- Don't retry 5xx errors
- In Production
	- Performance watchpoints
		- External User load
			- Most frequent and slowest requests
		- Periodic load
			- Traffic over an extended period of time
			- Confirm business reason for the load
		- Malicious Load
			- Source of traffic is expected and legitimate
			- Confirm agents asking for the web
	- Review deployment settings
		- Scaling
			- Autoscaling policies for traffic volumes
			- Set target utilization levels
		- Region
			- Source of traffic
			- Determinate bulk of traffic
		- Cron jobs
			- Schedule accurately

# Monitoring

- Dynamic config and intelligent defaults
- Platform, system, and application metrics
	- Ingest data: metrics, events, metadata
	- Generates insights through dashboards, charts, alerts
- Uptime/health checks
- Dashboards
- Alerts
- Workspace
	- Root entity that holds monitoring and configuration information
	- Determine your monitoring needs up front
	- Consider using separate workspaces for data and control isolation
- Alerting policies can notify of certain conditions
- Uptime checks test the availability of public services

```bash
# Installing monitoring agent on an instance
curl -O https://repo.stackdriver.com/stack-install.sh sudo bash stack-install.sh --write-gcm
```

## Logging
- Platform, systems, and application logs
	- API to write to logs
	- 30-day retention
- Log search/view/filter
- Log-based metrics
- Monitoring alerts can be set on log events
- Data can be exported to Cloud Storage, BigQuery, and Cloud Pub/Sub

```bash
# Install logging agent
curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh sudo bash install-logging-agent.sh
```

## Error Reporting
- Aggregate and display errors for running cloud services
	- Error notifications
	- Error dashboard

## Tracing
- Tracing System
	- Displays data in near real-time
	- Latency reporting
	- Per-URL latency sampling
- Collects latency data
	- App Engine
	- Google HTTP(S) load balancers
	- Applications instrumented with the Stackdriver Trace SDK

## Debugging
- Inspect an application without stopping it or slowing it down significantly
- Debug snapshots
	- Capture call stack and local variables of a running application
- Debug options: 
	- Inject lo

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODcxMjEzNDE4LC03OTg2NDk0ODksNTUyNT
U5ODA4LDgyNjQyMTU0MiwtMTM5NjMxODAxOSwxODY5MTg5OTcz
LC0xNTYzMjUwNzg5LC0xNDY2OTUxNDE1LC0xNjQwNDI1MTg2XX
0=
-->