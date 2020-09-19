
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

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTIyMDk1MywxNzgyODI0MjkxXX0=
-->