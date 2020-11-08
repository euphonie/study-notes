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



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNTA3NjIyMDIsMTQ1Mzk0Njg2MF19
-->