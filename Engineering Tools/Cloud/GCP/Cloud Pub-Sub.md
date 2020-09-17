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
- **Poll subscription**
	- Subscriber controls rate of delivery
	- Acknowledgement de

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExNzIyOTgyMCwxNzczNzY4NzU1XX0=
-->