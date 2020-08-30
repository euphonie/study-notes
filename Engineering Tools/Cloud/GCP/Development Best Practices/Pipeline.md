
# Best Practices

- Inside Code repository
	- Don't store dependencies, rather use dependencies managers
- Don't store configuration settings as part of code, instead configure them as environment variables
- Instead of monolithic architectures consider implementing microservices architectures.
	- Individual services can be modified, updated and deploy on its own
- Keep UI responsiveness by performing backend operations asynchronously and using event processing
	- Using Cloud Storage to store an image, and having Cloud Functions to process the image and upload thumbnails to other buckets
- Design with a Cloud Pub/Sub (Message Queue) component in mind
- Implement stateless components for scalability
	- Workers perform compute tasks without sharing state and can scale up and down reliably
- Cache content for improvement on application performance and lower network latency
	- CDN can also be used to cache pages coming from Compute Engine or static content from Cloud Storage
- Implement API gateways to expose backend functionality to consumer applications
	- Cloud Enpoints or Apigee

**Federated Identity Management**
- Delegates user authentication to external Identity Providers such s Google, Fb, Twitter or Github. Minimize effort for user administration. 
- No need to implement, secure, and scale a propietary solution for authenticating users

**Implementing health-check endpoints**
- Monitoring data can be used to automatically alert operations teams as soon as the system begins to fail
- Teams can diagnose and address the issue promptly
- Define the level of failure for each component that is being checked, as if when a non-critical component is failing the specific health check will return a warning but the overall health check from the service will return a healthy status

**Logging and Monitoring**
- StackDriver can log and send alert if a threshold is met
- Logs can be treated as event streams
- Don't keep log files but leverage the event stream for further analysis and storage
- It can help in
	- Debugging
	- Error Reporting
	- Tracing
	- Logs-based metrics
	- Monitoring
- Errors can be categorized
	- Transient 
		- Retry with exponential backoff 
		- Fail gracefully if error persists
	- Long lasting (Service availability)
		- Applications should not waste CPU cycles
		- They should implement a circuit breaker and handle the failure gracefully
	- For user-facing errors, consider degrading the experience gracefully instead of displaying an error message

**Data sovereignty and compliance requirements**
- Regions and industry segments have strict compliance requirements for data protection and consumer privacy

**High availability testing and Disaster Recovery plans**
- Testing env
	- Identify failure scenarios
	- Create disaster recovery plans (people, processes, tools)
	- Perform tabletop tests
		- Teams discussed how they would respond in failure scenarios but don't perform any real actions
		- What to do in unexpected situations
		- Simulate failures and address problems and refine the disaster recovery plan
- Production env
	- Perform canary testing and blue/green deployments
		- Tests during a maintenance window or during off-peak hours to minimize the impact
	- Validate your disaster recovery plan
- Principal failure scenarios
	- Connectivity failure
	- On-permises data center or other cloud-provider failure
	- GCP zonal or regional failure
		- Uncommon or rare
	- Deployment rollback
	- Data corruption caused by network or application issues
- During failure check, see the correct people were contacted and the traffic was rerouted using redundant routes and that data was not corrupted

**Implement CI/CD pipelines**
- Reduce regression risk
- Have more releases
- Improve release delivery time
- Manage rollbacks
- Process
	- Code stored in control version systems
	- Push code triggers a build and testing environment like Jenkins to build and run tests
	- Build system produces deployment artifacts for all required runtime environments
	- Deployment systems, like Spinnaker, automatically trigger the deployment of builds to test environments
		- Automatically execute integration, security and performance tests 
	- Finally deploy a successful build to production
		- Consider canary testing or blue/green testing to reduce the affected users if an issue is encountered
	- Setup performance metrics and alerts to monitor production
- SecDevOps
	- Automate security checks in the pipeline
	- Check third-party software and dependencies security
	- Scanning code for vulnerabilities
	- Confirm resources have least privilege permissions
	- Detecting errors in production and rolling back

**Re-architecturing applications**
- Strangler pattern
	- Replace smaller parts of an application with newer application components or services
	- Strangler facade can receive requests and direct them to the old application or the new services
	- Minimizes risk

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODIyODMwMSwxNjY2ODI3MzYwLDg3Nj
I5NzIzNCwtMzI3NzgwNzQzLC0xNTU1MzU0NzQ2XX0=
-->