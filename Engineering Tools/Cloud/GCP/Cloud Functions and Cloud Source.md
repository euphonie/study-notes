
# Cloud Source

Repositories that provide a git version control to support the team's development of any application or service, including those that run on App Engine, Compute Engine, and Kubernetes Engine. 
- Contains a source viewer

# Cloud Functions

Serverless environment where logic can be executed on demand and in response to different events.

Code in any language for a given runtime environment that GCP provides and then can be configured when it needs to be fired.
- Works with event-driven functions
- Payment fees stick to whenever the function runs in 100 millisecond intervals.
	- Priced according to how long function runs, the number of times it's invoked and the resources that you provision for the function
- Can trigger on events in
	- Cloud Storage
	- Cloud Pub/Sub
	- or HTTP calls
- The event that calls a cloud function is called **trigger**
- Cloud functions can be triggered from GCP emitted events or external services invoking an specific functions
	- They can in turn, trigger other APIs or GCP resources
- Functions can be triggered asynchronously and are called **Background Functions**
	- Synchronous functions are called **HTTP Functions**
		- Timeout default is 60 seconds

## Creating functions
- Write function
	- Select language
	- Define dependencies in a file
	- Select type of function
		- HTTP functions
			- Request
			- Response
		- Background functions
			- Takes an event 
			- and a callback
	- Local /tmp disk mount is provided for temporary file processing
		- Clean up temp files as they might consume the allocated memory
- Deploy code
	- From local machi

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNzIxMzE3MDcsLTIwMTIyMDk1MywxNz
gyODI0MjkxXX0=
-->