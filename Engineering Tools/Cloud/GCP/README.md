# Google Cloud Platform

Content sections
- IAM
- Networking
- Storage

## Deployment: Infrastructure as a Code

It's better to define templates for infrastructure to follow a declarative strategy instead of an imperative (introducing each command per each desired action)

GCP uses **Deployment Manager** (Infrastructure management service) to let users work in this way. Works with a YAML template file or a python file.

## Proactive monitoring

Monitoring lets you figure out whether the changes you made were good or bad.
It lets you respond with information rather than with panic. GCP works with Stackdriver for monitoring, logging and diagnostics.
	- Infrastructure platforms, VMs, containers, middleware and application tiers, logs, metrics and traces.
	- Core components
		- Monitoring. Checks endpoints of web apps and other internet accessible services. Uptime checks, alerts and use with notification tools.
			- Allows dashboard creation to visualize the state of an application
		- Logging. View logs from appl
		- Trace
		- Error Reporting
		- Debugging

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwNjI0MTU4NywxMTcwNzUyNTgzLC01ND
QyNDcxNTUsLTg1MTUxMzY0OSw3NDUzOTg2ODBdfQ==
-->