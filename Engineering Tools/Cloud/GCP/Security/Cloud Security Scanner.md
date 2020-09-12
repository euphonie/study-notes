# Cloud Security Scanner

- Web scanner for common vulnerabilities
- It scans
	- XSS
	- Flash injection
	- Mixed content
	- Clear text passwords
	- Use of insecure Javascript libraries
- Scans can be setup, schedule (manual or automatic)
- Duration depends on size and complexity
- Generates a load against the application
- Will probably change state in the application so it may be used with caution
	- Run scans in test environment
	- Using test accounts
	- Use backup data to restore a test after scan
- Process
	- Navigates every link it finds
		- Certain URL patterns can be blocked
	- Activates every control and input
	- Logs in with specified credentials
	- User-agent and maximum Request per rate (Queries per second, QPS) can be configured

**Cloud IAP**
- Central authentication and authorization layer for all applications over HTTPS. 
	- Replaces the need of using VPN tunnels or apply authentication and authorization for an specific application.
- Process
	- Request is forwarded to the Cloud IAP Proxy, which requires the user to login
	- Once logged in, the proxy will determine if the user is allowed to access that application, if they are, they are then forwarded to the requested application page
- Lets manage access to App Engine, Compute Engine and GKE clusters.

## Application Vulnerabilities

- **Injection**. Happens when some form of malicious content can be injected into an application from an app attacker and then the application accepts and interprets the content.
	- SQL
	- LDAP
	- HTML
- **Cross-site scripting**. A form of injection where the attacker is able to inject javascript into an application, and the code injection originates from a different site. Used to hijack user sessions, deface user websites and redirect the user to other malicious sites.
- **Weak authentication and access control**. Authentication, access control and session management are application logic functions which are often implemented insecurely. This can allow attackers to compromise passwords, keys or session tokens to exploit flaws and assume the users' identities.
- **Sensitive data exposure**. Sensitive data is not protected and therefore, can be exploited by attackers for credit card fraud, identity theft and other data and identity crimes.
	- Sensitive data should always be transferred with extra protection. It requires encryption at rest and in transit, and special precautions when exchanged with the browser.
- **Security misconfiguration**. Is commonly a result of default configurations, incomplete or ad-hoc configurations, open cloud storage, misconfigured HTTP headers and also verbose error messages with sensitive information.
	- All tools and environments should be patched and updated.
- **Using components with known vulnerabilites**
- **Phishing attacks**
- **OAuth phishing**. Is executed by tricking users to granting persistent access to their user accounts.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwNzg3MzI2NiwxOTYyMTg1MTE0XX0=
-->