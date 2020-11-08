
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

## Reliability
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
	- Reliably recover when users delete data by mistake
		- Move deleted data to trash, can be restored in usually less than 30 days
		- Application deletes data and moves to soft-deletion, can be restored in  usually less than 60 days
		- Application purges data and moves to hard-deletion, data is gone

## Disaster Planning

- High availability
	- Deploy multiple servers
	- Orchestrate servers with a regional managed instance group
	- Create a failover database in another zone or use a distributed database like Firestore or Spanner
	- Kubernetes clusters can also be deployed to single or multiple zones
	- When using instance groups create a health check to enable auto healing
		- Create a test endpoint in your service
		- Test endpoint to verify service is up
		- If health check fails, instance group will create a new server and delete the broken one
		- Load balancers use health checks too
	- When using Cloud SQL, create a failover replica for high availability
		- Replica will be created in another zone in the same region as the database
		- Will automatically switch to the failover if the master is unavailable
		- Doubles the cost of the database
	- Spanner and Firestore can be deployed to 1 or multiple regions
- Consider risk/cost analysis
	- Compare Deployment (Single zone, multiple zones in a region, multiple regions), estimate cost, availability % and cost being down

### Disaster Recovery strategies

- Cold standby
	- Create snapshots, machine images, and ata backups in multi-region storage
	- If main region fails, spin up servers in backup region
	- Route requests to new region
	- Document and test recovery procedure regularly
- When disaster planning, brainstorm scenarios that might cause data loss and/or service failure
	- What could happen that would cause a failure?
	- What is the Recovery Point Objective (amount of data that would be acceptable to lose)?
	- What is the Recovery Time Objective (amount of time it can take to be back up and running)?


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzNTczMzcyMSwtMTA4NjAwOTkyMl19
-->