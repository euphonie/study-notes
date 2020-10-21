
# Deployment Manager

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
eyJoaXN0b3J5IjpbODU2ODg5NTRdfQ==
-->