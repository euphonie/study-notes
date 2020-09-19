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
		- w/Firebase, auth0, and Google authentication
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
	- Registers with the service management API and shared with the Extensible Service Proxy
	- Service management API uses host to create a new Cloud Endpoint service with format `[YOUR-API].endpoints.[YOUR-PROJECT-ID].cloud.goog`
	- Uses DNS compatible names to uniquely identify services
	- Project ID can be used to name the API as it's unique
	- Extensible Service Proxy is a nginx proxy and injects authentication, monitoring and logging
	- The extensible service proxy validates the configuration with the Service Control API at runtime and determines if it can go through to the API backend
	- Service Control API logs information about incoming requests
	- This gives a Service Configuration ID and Service Name
	- Permissions can be granted to users or groups by IAM roles to specific endpoints
- Deploy API backend
- Good practices
	- For every change use the version on the API specification for tracking, this is for backwards compatible changes
	- For breaking changes deploy multiple versions of an API using different YAML files named after the version. For example: `apiconfig_v1.yaml` and `apiconfig_v2.yaml`
- **Environments**
	- Development: `[API].jane-dev-project.cloud.goog`. For running development tests
	- Staging: `[API].staging-project.cloud.goog`. For running integration tests
	- Production Alpha: `[API].prod-alpha-project.cloud.goog`
	- Production: `[API].prod-project.cloud.goog`

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTc5NzAxNTQsMjA1MDA3OTM1NywtMTg2OD
A5MjU2MF19
-->