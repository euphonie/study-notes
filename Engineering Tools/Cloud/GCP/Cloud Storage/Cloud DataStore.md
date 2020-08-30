
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
eyJoaXN0b3J5IjpbLTE3NzU5NjkwOTksLTE3ODY5MzU4OF19
-->