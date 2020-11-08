
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
	- Plan to have one unit out for upgrade or testing and survive another failing: N+2L


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyNzk0MjY5Ml19
-->