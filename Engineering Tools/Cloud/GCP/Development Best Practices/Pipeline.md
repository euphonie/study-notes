
# Development Best Practices

## Managing code and environment 
- Inside Code repository
	- Don't store dependencies, rather use dependencies managers
	- Don't store configuration settings as part of code, instead configure them as environment variables
	- Instead of monolithic architectures consider implementing microservices architectures.
		- Individual services can be modified, updated and deploy on its own
	- Keep UI responsiveness by performing backend operations asynchronously and using event processing
		- Using Cloud Storage to store an image, and having Cloud Functions to process the image and upload thumbnails to other buckets
	- Design with a Cloud Pub/Sub (Message Queue) component in mind
	- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2Mzc2ODA1MTUsLTE1NTUzNTQ3NDZdfQ
==
-->