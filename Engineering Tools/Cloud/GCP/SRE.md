
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

- **Avoid single point of failure**
	- Define unit of deployment 
	- Plan to have one unit out for upgrade or testing and survive another failing: N+2L ( A spare spare  N+2) 
	- Each unit should be able to handle extra load
	- Single units shouldn't be too large
	- Make units interchangeable stateless clones
- **Beware of correlated failures**
	- Occur when related items fail at the same time
	- if a zone or region is lost, all the resources in it fail
	- servers on the same software run into the same issue
	- if a global configuration system fails, and multiple systems depend on it, they potentially fail too
	- The group of related items that could fail together is called a **failure domain**
	- **To avoid**
		- Divide business logic into services based on failure domains
		- Deploy to multiple zones/regions
		- Split responsibility into components and spread over multiple processes
		- Design independent, loosely coupled but collaborating services
- **Beware of cascading failures**
	- Occur when one system fails, causing others to be overloaded. 
	- **To avoid**
		- Use health checks in Compute Engine or readiness and liveliness probes in Kubernetes to detect and then repair unhealthy instances
		- Ensure that new server instances start fast and ideally don't rely on other backend/systems to start up
- **Query of death overload**
	- Business logic error shows up as overconsumption of resources, and the service overloads, Solution: Monitor query performance. Ensure that notification of these issues gets back to the developers.
- **Positive feedback cycle overload failure**
	- The dev makes the system more reliable by adding retries, and instead you create the potential for an overload. Solution: Prevent overload by carefully considering overload conditions whenever you are trying to improve reliability with feedback mechanisms to invoke retries
- **Exponential Back-off**
	- If a service fails try again
		- Continue retry, but wait a while between attempts
		- Wait a little longer each time the request fails (exponential back-off)
		- Set a maximum length of time and a maximum number of requests
		- Eventually, give up
- **Circuit Breaker**
	- Protects service from too many retries
	- Plan for degraded state operations
	- If a service is down and all its clients are retrying, the increasing number of req can make it worse
		- Protect the service behind a proxy that monitors service health ( circuit breaker )
		- If the service is not healthy, don't forward requests
	- If using GKE, leverage Istio to automatically implement circuit breakers
- **Lazy deletion**


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2ODAzODkzNTMsLTEwODYwMDk5MjJdfQ
==
-->