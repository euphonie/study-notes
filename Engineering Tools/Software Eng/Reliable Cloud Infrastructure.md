
# Reliable Cloud Infrastructure

> Template: [Design and Process Workbook from Google ](https://docs.google.com/presentation/d/1gg6PTfgLNqh6CKXZ-k-HjHGKq5n3uz9OBXBG_K43TC4/edit?usp=sharing)
> Google API Design Guide: [Link](https://cloud.google.com/apis/design)

## Steps

### 1. Defining a case study
- Add a brief description
- List a few main features
- List roles of typical users

### 2. Requirements, analysis and design

**Requirements analysis**
| Who | Determining not only the user of the system, but developers and stake holders. Who the systems affects directly and indirectly  | Who are the user? Who are the developers? Who are the stakeholders? |
|--|--|--|
| What | Establish the main areas of functionality required in a clear unambiguous manner | What does the system do? What are the main features?|
| Why | What is a problem the proposed system aims to address or solve? Without a clear understanding extra requirements will certainly be added. This will potentially help in defining KPIs, SLOs and SLAs | Why is the system needed? |
| When | Helps determine a realistic timeline and can help contain the scope | When do the users need and/or want the solution? When can the developers be done? |
| How | Helps determine non-functional requirements | How will the system work? How many users will there be? How much data will there be?  |

**Roles**
- Represet the goal of a user
- Are not people or job titles
	- People and roles have a many to many relationship
	- Should describe a users objective. What does the user want to do?
- For more important roles a **Persona** can be created
	- Is an imaginary representation of a user role
	- Personas tell a story of who they are
	- Describe a feature from the user's point of view
		- Give each story a title that describes its purpose
		- Write a short, one sentence description
		- Specify the user role, what they want to do, and why
		- Use the template: As a [role], I want to..., so that I can....
			- Alternative: Given...[context], When I do...., then .... should happen.
		- Ex. **As an** account holder, **I want to** check my available balance at any time of day **so** I am sure not to overdraw my account

**Invest Criteria for evaluating user stories**
- INVEST
	- **Independent**. Prevent problems with priorization and planning
	- **Negotiable**. Used to stimulate discussion between customer and developers until there is a clear agreement, they add collaboration.
	- **Valuable**. Stories should provide value to users. Think about outcome impact, not outputs and deliverables.
	- **Estimatable**. If is not estimatable, there are missing details or the story is too large.
	- **Small**. Keeps scope small and less ambiguous, supports fast feedback
	- **Testable**. This way developers can verify that the story has been implemented correctly and validate when requirement has been met/ is done.


###  3. KPIs
- Metrics that can be used to measure success
- Not the same as a goal or objective, the goal is the outcome or result wanted to be achieved, the KPI is a metric that indicates whether you are on track to achieve the goal
- For each KPI, define targets for what success looks like, allows readjustment based on monitoring and feedback
- To be must effective they should be accompanied by a goal
- Common Business KPIs
	- Return on Investment, ROI
	- Earnings before interest and taxes, EBIT
	- Employee turnover
	- Customer churn
- Common Software (Technical) KPIs
	- Page views
	- User registrations
	- Clickthroughs
	- Checkouts
- Must be SMART
	- Specific
	- Measurable. Monitoring can indicate if you're moving towards or away from the goal
	- Achievable
	- Relevant. Does it really matter to the user? Will it help achieve application goals?
	- Time-bound. Helps measing the KPI. Per year/month/day?

### 4. Serice Level

**SLI (Indicators)**
- Measurable attribute of a service. A KPI.
- Quantitive measure
- Percentiles are better to measure SLIs, where a high order percentile, such as 99% shows worst-case values. While the 50th percentile indicates a typical case

**SLO (Objectives)**
- Number or the goal you want to achieve for a given SLI for a given duration
- 95% availability per day
- Stated as target/lower bound <= SLI <= upper bound
- Should specify how they are measured and the conditions when they are valid
- Multiple SLOs can be specified for the 50%, 98% and 99.9% cases.
- Ex. Average latency of HTTP requests for a service should be less than 100 milliseconds
- **Tips**
	- The goal isn't to mak the SLOs as high as possible but as low as you can get away with while still making users happy
	- The higher the SLO is the higher the cost in compute resources and operations effort
	- It is better to have lower SLOs to begin with and tighten them over time as you learn about the system
	- Avoid absolute values, SLOs with 100% is unrealistic, this increases time to build, complexity and cost to operate and might be highly unlikely to be required
	- Applications should not significantly outperform their SLOs, because users come to expect the level of reliability you usually give them
	- Minimize SLOs, common mistake is having too many. Have just enough to give coverage of the key system attributes

**SLA (Agreements)**
- Agreement between service provider and consumer
- Binding contract providing the customer compensation if the service doesn't meet specific expectations. More restrictive version of the SLO.
- Not every service has SLAs, but every service should have SLOs
- SLAs should be conservative, is difficult to remove SLAs that offer little value or cause a large amount of work. Setting them too high, can result in unnecessary compensation being paid
- An SLA should have a threshold that is lower than the SLO

**Example**
- SLI: The end-to-end latency of successful HTTP responses (HTTP-200)
	- This are averaged over 1 minute
- SLO: The latency of 99% of the responses must be <= 200 ms
- SLA: The user is compensated if 99th percentile latency exceeds 300 ms
	- A buffer exists over the SLO, even if SLO is exceeded there is some capacity before the SLA is broken

### 5. Microservice Design and Architecture

- Main reasons to choose architecture
	- Enable teams to work independently and deliver through to production at their own cadence
		- This supports scaling the organization
		- Adding more teams
		- Increases speed
	- Being able to scale the microservices independently based on their requirements
- Things to take into account
	- Strong contracts need to be defined between microservices
	- Allow for independent deployment cycles and rollback
	- Facilitate concurrent AB release testing on subsystems
	- Minimize test automation and quality assurance overhead
	- Improve clarity of logging and monitoring
	- Provide fine-grained cost accounting
- Pros
	- Easier to develop and maintain
	- Reduced risk when deploying new versions
	- Services scale independently to optimize use of infrastructure
	- Faster to innovate and add new features
	- Can use different languages and frameworks for different services
	- Choose the runtime appropriate to each service
- Cons
	- Increased complexity when communicating between services
	- Increased latency across service boundaries and resilience for failures
	- Concerns about securing inter-service traffic
	- Multiple deployments
	- Need to ensure that you don't break clients as versions change
	- Must maintain backward compatibility when clients as the microservice evolves
- Decomposing applications
	- Decompose by feature to minimize dependencies
	- Organize services by architectural layer
	- Isolate services that provider shared functionality
- Stateful services ave different challenges than stateless one
	- Stateful (Service, database)
		- Manage stored data over time
		- Harder to scale
		- Harder to upgrade
		- Need to back up
		- Best practices
			- Avoid storing shared state in-memory on your servers
				- Requires sticky sessions (session affinity) to be set up in the load balancer, Hinders elastic autoscaling
			- Store state using backend storage services shared by the frontend server
				- Cache state data for faster access
				- Take advantage of GCloud-managed data services (Firestore, Cloud SQL or memorytore for caching)
	- Stateless (UI)
		- Get their data from the environment or other stateful services
		- Easy to scale by adding instances
		- Easy to migrate to new versions
		- Easy to administer

**Best practices**
- 12 factor app, set of best practices
1. **Codebase**. Tracked in revision control, many deploys
	1. Each app has one code repo and vice cersa
2. **Dependencies**. Explicitly declare and isolate dependencies
	1. use package managers and declare dependencies 
	2. Isolate dependencies by packing them into a container
3. **Config**. Store config in the environment
	1. Don't put secrets, connection strings, endpoints, etc in source code
	2. Store those as environment variables
	3. Should be external to the code
4. **Backing services**. Treat backing services as attached resources
	1. Databases, caches, queues, and other services are accessed via URLs and set by configuration
	2. Should be easy to swap one implementation for another
5. **Build, release, run**. Strictly separate build and run stages
	1. Build creates a deployment package from the source code
	2. Release combines the deployment with configuration in the runtime environment
	3. Run executes the application
6. **Processes**. Execute the app as one or more stateless processes
	1. Apps run in one or more processes
	2. Each instance of the app gets its data from a separate database service
7. **Port binding**. Export services via port binding
	1. Apps are self-contained and expose a port and protocol internally
	2. Apps are not injected into a separate server like apache
8. **Concurrency**. Scale out via the process model
	1. Because apps are self-contained and run in separate process, they scale easily by adding instances
9. **Disposability**. Maximize robustness with fast startup and graceful shutdown
	1. App instances should scale quickly when needed
	2. If an instance is not needed, you should be able to turn it off with no side effects 
10. **Dev/prod parity**. Keep development, staging, and production as similar as possible
	1. Container systems like Docker makes this easier.
	2. Leverage infrastructure as code to make environments easy to create
11. **Logs**. treat logs as event streams
	1. Write log messages to standard output and aggregate all logs to a single source
12. **Admin processes**. Run admin/management tasks as one-off processes.
	1. Admin tasks should be repeatable processes, not one-off manual tasks
	2. Admin tasks shouldn't be a part of the application
 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5NDk4NDk1NCwyNzEzNzk1OTcsMTUyOT
I5Nzg2OSwtMjYwMTI0MDQxLDE0NDg0NDUxNDgsMTMzNzA4NTA0
NSwtMTY4NDU0OTk5XX0=
-->