# Cloud Endpoints

Helps create and maintain APIs, through an easy to deploy proxy in front of the software service, and provides an API console to wrap up the capabilities in an easy-to-manage interface.

- Controls access and validate calls with JSON web tokens and Google API Keys
	- Identify web, mobile users with Auth0 and Firebase authentication
- Generate client libraries
- Works in App Engine Flexible environment, Kubernetes Engine and Compute Engine
- Works with Android, iOS and javascript
- **Apigee Edge** can be used in migrations from monolithic to microservices by focusing in each unique service within the new infrastructure
- Areas of interest
	- Interface definition
		- Open API specification
			- Used with REST APIs
		- gRPC API specification
			- Generate client libraries
		- Support transcoding of HTTP JSON calls into gRPC
	- Authentication and Authorization
		- Service-to-service authentication
		- User authentication 
		- w/Firebase, OAuth, and Google authentication
	- Management and scalability
		- Extensible Service Proxy API
		- Service Management API
		- Service Control API
	- Logging and Monitoring
		- Stackdriver Logging
		- Stackdriver Trace

**Pipeline**
- Develop API backend
- Develop API configuration
	- YAML file using Open API specification
```yaml
swagger: "2.0"
info:
	description: "My new API"
	title: "Cloud Endpoints Example"
	version: "1.0.0"
host: "quiz-api.endpoints.YOUR-PROJECT-ID.cloud.goog"
basePath: ...
paths: ...
securityDefinitions: ...
```
- Deploy API configuration
	- This gives a Service Configuration ID and Service Name
- Deploy API backend

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTYwMTAxMTMsLTE4NjgwOTI1NjBdfQ
==
-->