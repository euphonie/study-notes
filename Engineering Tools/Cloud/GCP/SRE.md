
# Designing Reliable systems


- Key metrics
	- Availability. Percent of time a system is running and able to process requests
		- Achieved with fault tolerance
		- Create backup systems
		- Use health checks
		- Use white box metrics to count real traffic success and failure	
	- Durability. Odds of losing data because of a hardware or system failure
		- Achieved by replicating data in multiple zones
		- Do regular backups
		- Practice restoring from backups
	- Scalability. Ability of a system to continue to work as user load and data grow
		- Monitor usage
		- Use capacity autoscaling to add and remove servers in response to changes in load

**Recommendations**

- Avoid single point of failure
	- Define unit of deployment 
	- Plan to have one unit out for upgrade or testing and survive another failing: N+2L ( A spare spare  N+2) 
	- Each unit should be able to handle extra load
	- Single units shouldn't be too large
	- Make units interchangeable stateless clones
- Beware of correlated failures
	- Occur when related items fail at the same time
	- if a zone or region is lost, all the resources in it fail
	- servers on the same software run into the same issue
	- if a global configuration system fails, and multiple systems depend on it, they potentially fail too
	- The group of related items that could fail together is called a **failure domain**


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0MjU1NzMzMl19
-->