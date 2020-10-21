
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
  type: compu

```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODc0NTM5NDQ2XX0=
-->