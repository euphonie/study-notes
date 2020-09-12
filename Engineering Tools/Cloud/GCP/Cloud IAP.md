
# Cloud Identity Aware Proxy

- Controls access to your cloud applications running on GCP
- Verifies a user's identity
- Determines whether that user should be allowed to access the application
> image iap
- Establishes a central authorization layer for applications accessed by HTTPS
- Lets the user adopt an application level access control model instead of relying on network level firewalls
- Resources can be only be accessed trough the proxy by users in groups with the correct cloud IAM role.
	- Cloud IAP performs authentication and authorization checks when a user tries to access a secured resource
> image iapworks
- Precautions
	- Configure firewall and load balancer to protect against traffic that doesn't come from the 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODc3MzA2MzEyXX0=
-->