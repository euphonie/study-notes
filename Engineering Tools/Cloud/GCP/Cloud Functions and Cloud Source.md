
# Cloud Source

Repositories that provide a git version control to support the team's development of any application or service, including those that run on App Engine, Compute Engine, and Kubernetes Engine. 
- Contains a source viewer

# Cloud Functions

Serverless environment where logic can be executed on demand and in response to different events.

- Highly scalable
- Microservices that require a small piece of code
Code in any language for a given runtime environment that GCP provides and then can be configured when it needs to be fired.
- Works with event-driven functions
- First 2M requests are free
- Payment fees stick to whenever the function runs in 100 millisecond intervals.
	- Priced according to how long function runs, the number of times it's invoked and the resources that you provision for the function
- Can trigger on events in
	- Cloud Storage
	- Cloud Pub/Sub
	- or HTTP calls
	- Firebase
	- Stackdriver Logging
- The event that calls a cloud function is called **trigger**
- Cloud functions can be triggered from GCP emitted events or external services invoking an specific functions
	- They can in turn, trigger other APIs or GCP resources
- Functions can be triggered asynchronously and are called **Background Functions**
	- Synchronous functions are called **HTTP Functions**
		- Timeout default is 60 seconds
- When using node.js code the function must be exported in a module
- Only package.json file is needed to install dependencies
- Lightweight microservices
- Can be setup as webhooks

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
	- From local machine using gcloud goes to a staging bucket for deploy
	- Using gcloud from a repository (cloud source) mirrored github or bitbucket
- View output
	- In stackdriver logging
	- In stackdriver error reporting for any errors
- View dashboard in cloud functions
	- Number of invocations
	- Execution times
	- Memory usage

# Cloud Dataflow

- Serverless execution engine or runner for executing parallel data processing pipelines that are developed using Apache Beam SDKs
- Supports fast and simplified pipeline development by using expressive Java and Python APIs in the Apache Beam SDK
- Integrates with GCP services 
	- for streaming events ingestion using Cloud Pub/Sub 
	- and data warehousing using BigQuery
	- with machine learning APIs and more
- A pipeline comprises the entire data processing tasks including reading input data, transforming the data and writing output data
- Uses CE, Stackdriver Logging, Clous Storage, BigQuery, Cloud Pub/Sub and Cloud Firestore APIs to execute the pipelines
- Supports simple configuration and optimizes the work account over time
- Auto scales based on CPU utilization, throughput and amount of remaining work
- Adds workers when CPU utilization and backlog increases and removes them when the metrics decrease
- Ideal for streaming and batch data pipelines
- Good for
	- clickstream POS
	- segmentation analysis in retail industry
	- Fraud detection in financial services
	- Personalized user experience in gaming industry
	- IOT analytics in manufacturing, healthcare and logistics industries

# Cloud Run

- Managed compute platform 
- Enables to run stateless containers that are invokable via web requests or Cloud Pub/Sub events
- Serverless
- Built on Knative
- Lets you run containers either fully managed or in own GKE cluster
- Containers offer flexibility and portability of workloads
- Work in any language using any tools
- Automatic scaling
- Only pay for time consumed
- Application must be stateless and respond through HTTP

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1MDQyNTYwMywzMzA1NzI1NDEsLTExMD
U4NzkwNzYsNTQ5MjE5MDg0LC0yMDEyMjA5NTMsMTc4MjgyNDI5
MV19
-->