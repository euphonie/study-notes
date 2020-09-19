
# Cloud Identity Aware Proxy

- Controls access to your cloud applications running on GCP
- Verifies a user's identity
- Determines whether that user should be allowed to access the application
> image iap
- Establishes a central authorization layer for applications accessed by HTTPS
- Lets the user adopt an application level access control model instead of relying on network level firewalls
- Resources can be only be accessed trough the proxy by users in groups with the correct cloud IAM role.
	- Cloud IAP performs authentication and authorization checks when a user tries to access a secured resource

- Precautions
	- Configure firewall and load balancer to protect against traffic that doesn't come from the serving infrastructure
	- Use signed headers or the App Engine standard environments Users API

## Firebase Authentication (Google's Federated Authentication)
- Supporting users sign in from using third-party credentials in the Client App.
- Process
	- Get authentication credentials from the user
		- These can be a username and password, or an OAuth token from a federated identity provider
	- Pass the credentials to the Firebase Authentication SDK
	- Firebase backend services verify credentials and return a response to the client
	- After successful sign-in the user can
		- Access the user's basic profile
		- Control the user's access to data stored in other Firebase products
		- Use the provided authentication token to verify the identity of users in your own backend services


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY3MTYyMjcyOCwtMTM4NzYwMzMzNV19
-->