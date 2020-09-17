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
- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwNTMxNzg5LDE3NzM3Njg3NTVdfQ==
-->