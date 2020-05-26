# Database design Methodology

> Notes created from content in **Udacity's Database Systems Concepts & Design**

## Stages of methodology

- **Analysis Stage**. 
	- Deliverable: Information Flow Diagram.
	- Info: Provided by the stakeholders while defining the end product.
- **Specification Stage**
	- Deliverables: Tasks and EER Diagram.
	- Info: Define EER diagram and identify processes needed to manipulate data within the structure.
- **Design Stage** 
	- Deliverables: Abstract Code w/SQL and Relational Schema
	- Info: Relational schema derived from ERD and code derived from tasks
- **Implementation Stage**
	- Deliverables: Code in Programming language and Relational schema in a DB


#  Schema concepts and organization of data

## ANSI-SPARC 
There are 3 levels of schema in which data can be represented inside a database:

### Internal Schema
- Describes hot information is physically represented to provide the overall best performance. E.g. indexes, sorting structures, etc.

### Conceptual Schema
- Describes conceptually relevant aspects of reality, might be seen as the description of the fields in a table. E.g. fields in a table.

### External Schema
- Derives from a conceptual schema and is used to provide an specific view to a group of users. E.g. views or procedures.



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTUyMzUzNjEsLTE1NDA2MTE1MDldfQ
==
-->