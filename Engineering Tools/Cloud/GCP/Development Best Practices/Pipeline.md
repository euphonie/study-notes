
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



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4MjczMjE1OCw4NzYyOTcyMzQsLTMyNz
c4MDc0MywtMTU1NTM1NDc0Nl19
-->