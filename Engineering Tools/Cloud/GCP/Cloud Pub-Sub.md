# Cloud Pub/Sub

A fully managed messaging architecture that enables you to build loosely coupled microservices that can communicate asynchronously. It can be used to integrate components of an application.

- Permits building multi-cloud or hybrid architectures.
- SDKs for many programming languages, sending messages through REST HTTP or gRPC 
- Open source Apache Kafka connectors
- Ideal for
	- Realtime gaming application
	- clickstream data ingestion and processing 
	- device or sensor data processing for health care and manufacturing
	- Integrating various data sources in financial applications
-  Can process large amounts of data and deliver it to Dataflow or BigQuery for analysis
- applications that publish messages are called **Publishers**
-  The repositories of messages are called **Topics**
- The application that receives messages is called **Subscriber** and subscribes to a topic. 
	- The subscription uses a **Push** or **Pull** method.
	- Messages are only received after the subscription was created, no previous messages
	- Subscriber sends acknowledgement when message received and processed.
		- After this, Cloud Pub/Sub removes the message
- If a subscriber doesn't acknowledges a message before the acknowledge deadline the message is resent
- Every message is delivered **at least once** to every subscription
- **Pull subscription** (Default subscription model)
	- Subscriber calls the pull method to request messages
		- Each message has an acknowledgement ID
		- To acknowledge the subscriber invokes the acknowledgeId method with the ID received
	- Subscriber controls rate of delivery
	- Acknowledgement deadline can be modified to allow more process time
	- Can handle multiple subscribers
	- Enables mass delivery and acknowledgements as well as massively parallel consumption
	- Ideal when there's a need to process a very large volume of messages with high throughput.
- **Push subscription**
	- Services don't need to implement Google Cloud Client Libraries to retrieve and process methods
	- Each message is sent as an HTTP request to the subscriber at a pre-configured HTTP endpoint
		- Endpoint can be a load balancer or App Engine standard application
	- Acknowledgement of the message is done by returning an HTTP success status code
		- An error indicates the message should be sent again
	- The rate of push requests is adjusted on the rate at which it receives success responses.
	- A default acknowledgement deadline can be configured
		- If message is not acknowledge before the deadline, the message is resent
	- Ideal when the GC libraries can't be configured or multiple topics must be processed by the same web hook.
	- Also ideal if HTTP endpoint processes messages from several QMSs
- Subscribers can be Cloud Functions, or deployed on CE, GKE or App Engine
- Elastic scaling can be enabled from StackDriver metrics
- Message Orde

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1OTE1NTMwMiwtMTc4ODI3MDA0MCwtMT
gyNjg3NjE0MCwxNDUwMDE3ODcyLDE3NzM3Njg3NTVdfQ==
-->