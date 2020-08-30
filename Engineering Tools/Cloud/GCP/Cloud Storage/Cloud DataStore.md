
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
	- Are defined in an index configuration file
- If property is not used in qu

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTE5ODc2MjY4XX0=
-->