# Designing Secure systems

- The client is responsible for certain actions
- Security is implemented in layers
	- Google provides tools that enable a secure environment

## Best practices
- Principle of least privilege
	- Use IAM to enforce the principle
	- Identify users with their login
	- Identify machines and code using service accounts
	- Assign IAM roles to users and service accounts to restrict what they can do
- Separation of duties
	- No one can change or delete data without being detected
	- No one can steal sensitive data
	- No one is in charge of design, implementation and reporting on sensitive systems
	- Use multiple projects to separate duties
	- Different people can be given different rights in different projects
	- Use folders to help organize projects
- Remove external IPs to prevent access to machines outside their network
	- Use a bastion host to provide access to private machines
	- Use Cloud NAT to provide egress to the internet from internal machines
	- All internet traffic should terminate at a load balancer, third-party firewall (proxy or WAF), API gateway, or IAP. 
- Configure firewall rules to allow access to VMs
	- By default, ingress on all ports is denied
	- Add firewall rules to control which clients have access to which VMs on which ports
	- Application level security is the responsibility of the consumer
- Control access to APIs using Cloud Endpoints
	- Protect and monitor your public APIs
	- Control who has access to your API
	- Validate every call with JSON Web Tokens and Google API keys
	- Integrates with Identity Platform
- Restrict access to your services to TLS only
	- All GCloud service endpoints use HTTPS
	- It's up to you to configure your service endpoints
	- In the load balancer setup, only create a secure frontend
- Leverage Google Cloud network services for DDoS protection
	- Global load balancers detect attacks and drop them
	- Enabling the CDN will protect backend resources
- Cloud Armor supports layer 7 web application firewall rules
	- Prevent SQL injection and cross-site scripting
	- Allow or deny traffic using request headers, geographic location, ip addresses, cookies, etc.
- Data Loss Prevention API can be used to protect sensitive data by finding it and redacting it
	- Scans data in Cloud Storage, BigQuery or Datastore
	- Can also scan images
	- Detects many different types of sensitive data, including: Emails, credit cards, tax IDs
	- Own information types can be added
	- Can delete, mask, tokenize, or just identifiy the location of the sensitive data


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzM3MjY4NDUsMTg0NzYyODQ1MiwtMT
I1MDc2MjIwMiwxNDUzOTQ2ODYwXX0=
-->