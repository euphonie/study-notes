
# Big Data Solutions

Integrated Serverless Platform. Custom solutions with google services to manage big data pipelines in the cloud.

## Big data
### Cloud Dataproc
- Managed Hadoop
- Based on MapReduce, it consists of a map function that runs in parallel with a massive dataset to produce intermediate results, and a reduce funciton which builds a final result set based on all those intermediate results.
- Fast, easy, managed way to run Hadoop and Spark/Hive/Pig on GCP
- Create clusters in 90s on average
	- Built on top of Compute Engine's VMs, the user chooses the number and type of machines
- Monitoring using Stackdriver
- Scale clusters up and down even when jobs are running
- Pay only for hardware resources used during the life of the cluster you create. Based on the hour but billed by the minute.
- Money can be saved using preemptible Compute Engine instances for batch processing.
	- Jobs need to be able to be restarted cleanly
- Spark/Spark SQL or MLib can be used for data mining or machine learning
### Pub/Sub

A messaging service for events in real time.
- Foundation for stream analytics 
- Supports many-to-many asynchronous messaging
- Application components make push/pull subscriptions to topics
- Include support for offline consumers
- Delivery at low latency
- Scalability to one million messages per second
- Messages might be delivered more than once
- Used for analyzing streaming data, from Cloud Dataflow for example.
- Subscribers can be notified for new messages or pool the data stream
- 

### Dataflow
For realtime data or unpredictable sized array. It's a unified programming model and a managed service that lets the user develop and execute a big range of data processing patterns (ETL and continuous computation).
- Builds data pipeline for batch and streaming data
- No need to spin up a cluster or size instances it's fully automatic management- 
- Ex. BigQuery can be used to extract data, data transformation is issued inside Dataflow and all data is then stored in a Cloud Storage acting as a sink.
	- Multiple map and multiple reduce operations
- Use cases. General purpose ETL tool, data analysis engine (fraud detection and financial services, IoT analytics and manufacturing, healthcare and logistics and click stream, PoS and segmentation analysis in retail)
- Can be used in real time applications

### BigQuery
Most useful when wanting to do ad-hoc SQL queries or exploration on a massive data set.
- Fully managed petabyte-scale, low-cost analytics data warehouse.
- Use familiar SQL
- Data can be feed from Cloud Storage, Cloud Data Store or streamed in at up to 100,000 rows per second.
- Easily read-write via Cloud Dataflow, Hadop and Spark
- SLA 99.99%
- BigQuery has a global scope
- The user can specify the region where the data is kept, just specifying the location.
- Storage is paid separately from queries, queries are only paid when running
- Data can be shared with other people and queries run by them are charged to their accounts
- Price drops of storage after 90 days

## Cloud Datalab (Jupyter)

- Interactive tool for large-scale data exploration, transformation, analysis, and visualization
- Integrated, open source
- Runs in a Compute Engine VM
	- The users specifies machine type and region
- Orchestrates multiple GCP services
- Pay only for resources used
- Integrated with BigQuery, Compute Engine, and Cloud Storage
- Data visualization with Google Charts or map plot line

## IA

### Machine Learning

Machine learning is one branch of the field of artificial intelligence. It's a way of solving problems without explicitly coding the solution.

### Vision

### Natural Language Processing

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1OTk0NjIwNiwtMjExMTIwODc5N119
-->