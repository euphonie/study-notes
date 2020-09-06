# Security in BigQuery

- BigQuery uses IAM for resources and permissions
- Tables, rows and columns are child resources of datasets and inherit their permissions
	- However you can't assign permissions at table, row or column level
	- All tables in a dataset share the same permissions
- Roles
	- Admin. can do everything. create and read data, run jobs, set IAM policies
	- Data Owner. read/write access to data, can grant access to other users and groups through IAM policies
	- Data Editor. read/write access to data
	- Data Viewer. read-only access to data
	- Job User. can create and run jobs, but no access to data
	- User. can run jobs, create datasets, list tables, save queries. But no default access to data
- Groups should be always preferred instead of assigning roles to every individual user to reduce overhead
- Creator is owner but other users can also be owners.
- **Authorized views**. can give access to only a subset of the data to a group of users.
	- Views provide row or column level permissions to datasets
	- Process
		- Create a copy of the dataset with different permissions from the original
		- Add a view that selects the subset of data you want to expose from the first dataset
		- Give the view the access to the underlying data in the first dataset




> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA3ODg2MjYyM119
-->