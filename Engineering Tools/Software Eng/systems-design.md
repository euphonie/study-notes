# The Well-Architected Framework (AWS)

## Main objectives 
- know capacity needs
- Test at production scale
- automate architectural experimentation
- evolutionary architecture
- use data to drive architecture
- improve through game days (experimentation)


## Pillars
### Operational Excellence

Operations as code -> IaC, pipelines
Frequent, small, reversible changes -> small & focused commits + trunk-based deployment/rollback
refine operations procedures frequently
anticipate failure (what to do when something fails)
learn from operational failures (post-mortem)

#### Best practices
Organization: understand  priorities, culture and model 
- evaluating customers' needs
- evaluating governance 
- evaluating threats

**Actions**
- telemetry
- design for operations (version control, test strategies, multiple environments)
- operational readiness and changes management (skill-gap)
- mitigate deployment risks (automate testing, automate rollback)

Operate: understand workload health, respond to events, understand operational health
- metrics
- evaluating patterns of work 
- push notifications 
- dashboards to communicate operation

Evolve: sharing, learning and improve
- continuous improvement/learning
- document and share your losses/wins

### Security

- strong identity foundation
- traceability
- security at all layers
- automate security best practices
- protect data in transit and at rest
- keep people away from data (principle of least-privilege)
- prepare for security events

#### Best practices
- IAM 
- Detection
- Infrastructure protection
- Data protection
- Incident Response

**Actions**
-  multi-factor authentication
- isolated workloads in different VPCs
- integrate users/permissions into roles
- use aws secrets
- acl's
- db encryption patterns/segmentation

### Reliability 

- automatic recover from failure
- test recovery procedures
- scale horizontally to increase aggregate workload availability
- stop guessing capacity
- manage change in automation

### Best practices
- monitor workload in demand to maintain optimal level
- changes to infra should use automation (change management)

**Actions**
- Foundations: manage server quotas and constraints, network topology
- workload architecture: micro-service arch, integrated, make components smaller, 
how to design interactions (develop to mitigate failures) 
= change management: monitor workload resources, adapt to demand and implementation
- failure management: backup data, design for disaster recovery


### Performance Efficiency
- democratize advanced technologies (utilize existing services/systems)
- go global in minutes (reduce latency)
- use serverless architecture (remove operational burden)
- experiment more often (experiment with multiple architectural components)
- consider mechanical sympathy (e.g., data access patterns on selecting databases)

#### Best practices
- performance architecture: what available services exist, how to choose arch, costs on decisions
- network architecture: leverage load balancing, keep location optimized (CDN/compute at edge)
- compute architecture: test diff compute choices, right sizing instances 
- database architecture: 
- storage architecture: data access patterns (document, structured/non)

**Actions**
- infrastructure as code
- deployment pipeline
- metrics
- performance test automatically
- load generation
- performance visibility
- visualization
- monitoring: generation, aggregation, realtime processing and alarming, storage and analytics

### Cost optimization
- implement cloud financial management
- adopt a consumption model (transient/persistent resources)
- measure overall efficiency
- stop spending money on undifferentiated heavy lifting
- analyze and attribute expenditure

#### Best practices 
- having cost thresholds
- monitoring
- running cost explorer 

### Sustainability
- understand your impact (electricity cost + carbon footprint)
- establish sustainability goals
- maximize utilization

#### Best practices
- region selection
- user behavior patterns
- soft & arch patterns
- data patterns (data retention policies)
- hw patterns (lifecycle policies)
- dev & deployment patterns (lifecycle policies)
