
# Best Practices

- Data objects are called entities
	- Comprise one or more properties
- Each entity has a unique key that contains
	- Namespace
	- Entity Kind
	- Identifier (string or numeric ID)
	- Ancestor path
		- The path from root entity to child entity
- Operations on one or more entities are called transactions and are atomic
- Entity can have parent
	- Without a parent is a root entity
- Does not support join operations, inequality filtering on multiple properties, or filtering on data based on results of a subquery
- Instead of table the concept is a Kind

**Naming conventions**
- Use UTF-8 characters for
	- Namespace names
	- Kind names
	- Property names
	- Key names
- Avoid slash in kind names and custom key names
- Avoid sensitive information in a Cloud Project ID 

**Reads and writes**
- Max write rate to an entity group is 1/second
- Avoid high read or write rates to keys that are lexicographically close
- Gradually ramp up to traffic to new Cloud Datastore kinds of portions of the keyspace
- Avoid deleting large numbers of entities across a small range of keys
-  Use sharding for higher rate of writes and replication for higher rate of reads
	- If faster writing is needed manual sharding can be implemented
		- Sharding limitations: 1 write/sec per entity group = transaction throughput
		- Split frequently updated entities across multiple kinds
- Reduce contention by
	- Building a sharded counter
		- Pick a shard at random to increment the counter
		- To know the total count, read all counter shards and sum their individual counts
- Replication can be used if need to use a higher read rate of a portion of the key range
	- N copies of the same entity can be stored, allowing an N times higher rate of reads
- Batch operations are preferred (reads, writes, deletes)
- Roll back failed transactions 
- Use asynchronous calls

**Indexes**
- Built-in
	- Automatically pre-define an index for each property of each entity kind
	- Are suitable for simple types of queries
- Composite
	- Index multiple property values for indexed entity
	- Support complex queries
	- Configurable through the `index.yaml`
		- Define all properties to be indexed and run `gcloud datastore create-indexes`
		- To delete, remove from `index.yaml` and run `gcloud datastore cleanup-indexes`
	- Are defined in an index configuration file
- If property is not used in query exclude it from indexes
	- Otherwise can incur in increased latency to achieve consistency and storage costs
	- Also using a lot of composite indexes can incur in the same 
- Large queries without indexes should be executed using BigQuery
- Don't use monotonically increasing keys

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI0NTk0MTkzOCwxMzE2MzgzNzA2LDEzMT
Q0NDYzMDQsLTE3NzU5NjkwOTksLTE3ODY5MzU4OF19
-->