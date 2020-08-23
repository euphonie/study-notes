# Google Cloud Platform

Content sections
- IAM
- Networking
- Storage

## Deployment: Infrastructure as a Code

It's better to define templates for infrastructure to follow a declarative strategy instead of an imperative (introducing each command per each desired action)

GCP uses **Deployment Manager** (Infrastructure management service) to let users work in this way. Works with a YAML template file or a python file.

```bash
# Create new deployments through a declarative file
> gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
# confirm status from deployments
> gcloud deplyment-manager deployments list
```


## Proactive monitoring

Monitoring lets you figure out whether the changes you made were good or bad.
It lets you respond with information rather than with panic. GCP works with Stackdriver for monitoring, logging and diagnostics.
	- Infrastructure platforms, VMs, containers, middleware and application tiers, logs, metrics and traces.
	- Core components
		- Monitoring. Checks endpoints of web apps and other internet accessible services. Uptime checks, alerts and use with notification tools.
			- Allows dashboard creation to visualize the state of an application
		- Logging. View logs from applications and filter and search on them. Define metrics, based on log contents into dashboards and alerts. 
			- Receives from BigQuery, Cloud Storage and Cloud Pub/Sub.
		- Trace. Sample latency of app engine applications and report Per-URL statistics
		- Error Reporting. tracks and groups the errors in your cloud applications. Notifies new errors. 
		- Debugging. Connects application production data to the source code. Lets inspect the state of the app at any code location in production. Works best when code is in Cloud Source repositories

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI2MTAyODc3MSwxMTE2MDQxNTk1LDExNz
A3NTI1ODMsLTU0NDI0NzE1NSwtODUxNTEzNjQ5LDc0NTM5ODY4
MF19
-->