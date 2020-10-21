
# Deployment Manager

- Enables deployment of VM instances on container images that are created by the build pipeline
- Can also launch other GCP resources required by the application
- A deployment configuration file defines the Cloud resources to provision
	- Includes types and properties of the resources
	- Consists of a top-level configuration file, YAML templates and additional files
	- Templates can be developed using Jinja or Python syntax
- Benefits
	- Reuse templates and configure resources differently for different environments 
	- Specify dependencies on resources
	- Specify startup scripts run when the VM launches
- Infrastructure deployment service that automates the creation and management of GCP resources
- Provides repeatable deployment process with consistent results
- Declarative language, allows configuration and lets system to figure out steps
- Focus on the application
- Parallel deployment
- Template-driven
- Templates need to have a name, type and properties

```python
# example autonetwork
# autonetwork.jinja
resources: 
- name : {{ env["name"] }}
  type: compute.v1.network
  properties: 
	  autoCreateSubnetowrks: true
```
```python
# firewall.jinja
resources:
- name: {{ env["name"] }}
  type: compute.v1.firewall
  properties:
	  network: {{ properties["network"] }}
	  sourceRanges: ["0.0.0.0/0"]
	  allowed:
	  - IPProtocol: {{ properties["IPProtocol"] }}
	    ports: {{ properties["Port"] }}
```

```yaml
# config.yaml
imports:
- path: autonetwork.jinja
- path: firewall.jinja

resources:
- name: mynetwork
  type: autonetwork.jinja
- name: mynetwork-allow-http
  type: firewall.jinja
  properties: 
     properties:
         network: ${ref.mynetwork.selfLink}
         IPProtocol: TCP
         Port: [80]

```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI3MzY2ODQxMiw4NTY4ODk1NF19
-->