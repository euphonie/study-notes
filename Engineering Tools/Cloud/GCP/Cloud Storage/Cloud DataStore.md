
# Best Practices
1
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

**Transactions**
- Atomic (all applied or none)
- Max duration: 60s
- Idle expiration 10s after 30s
- Can fail when
	- Too many concurrent modifications are attempted on the same entity group
	- They exceed a resource limit
	- Datastore encounters an internal error
	- Datastore operations in a transaction operate on more than 25 entity groups
- Make transactions idempotent, so when a transaction is repeated the end result will be the same and has no additional effects with same parameters
- Success responses 200 and errors in 400 or 500

**Naming conventions**
- Use UTF-8 characters for
	- Namespace names
	- Kind names
	- Property names
	- Key names
- Avoid slash in kind names and custom key names
- Avoid sensitive information in a Cloud Project ID 
- For numeric keys
	- Don't use negative numbers
	- Don't use value 0
	- Get a block of IDs using the allocatedIds() method if you want to assign your own numeric IDs
	- Avoid monotonically increasing values (can create hotspots)

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
- Use cursors instead of offsets
	- Retrieve a query's results in convenient batches
	- Don't incur the overhead of a query offset
- Use query types

![Query types](https://raw.githubusercontent.com/euphonie/study-notes/master/Engineering%20Tools/Cloud/GCP/querytype.png)

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
eyJoaXN0b3J5IjpbLTE3ODcyNTMyMTAsOTA4MDUyNzQ3LC0xOD
ExMzc1MzU0LDEzMTYzODM3MDYsMTMxNDQ0NjMwNCwtMTc3NTk2
OTA5OSwtMTc4NjkzNTg4XX0=
-->