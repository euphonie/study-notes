# Google Kubernetes Engine

## Introduction

Orchestration platform to manage containers in clusters.

GKE stands in between Compute Engine as a IaaS and App Engine as a PaaS. 

GKE works around containers which give you the abstraction needed to run and scale your application without worrying on resource deployment, and the flexibility of IaaS solutions to manage the interrelations between the processes being run. 

Containers are alike to virtual machines but save the time and resources needed from booting up high-cost operating systems, to have a more process-like starting experience.

Kubernetes makes it easy to orchestrate many containers on many hosts. It helps to scale them, roll out new versions of them, and even roll back to the old version if things go wrong.

For building container images there are two options
- Docker
- Google Cloud Build

Containers
- start much faster than virtual machines
- abstract unimportant details of their environments
- can have different sized container images
- need a lightweight container runtime
- consumes less resources and is less error-prone than VMs
- are easy to move around

Example of a Dockerfile

```docker
FROM ubuntu:18.10
RUN apt-get update -y && \
	apt-get install -y python3-pip python3-dev
COPY requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip3 install -r requirements.txt
COPY . /app
ENTRYPOINT ["python3", "app.py"]
```

Create and image and run container
```bash
# Images can be uploaded to Google Container Registry
> docker build -t py-server
> docker run -d py-server
```

## Kubernetes

Opensource orchestrator for containers to better manage and scale applications.
- Has an API that allows authorized people to control its operations through several utilities. Ex. **kubectl** command
- Lets deploy containers on a set of nodes called a cluster
	- A cluster is a set of master components that control the system and a set of nodes that represent the computing instances
	- In GCP, nodes are VMs running in CE

## GKE

- Kubernetes as a managed service in the cloud
- Support different machine types, numbers of nodes and network settings
- **Pod**
	- Abstraction used to deploy containers
	- Is the smallest deployable unit in Kubernetes
	- Is usual to have only one container in a pod, but containers with hard dependencies can be packaged inside one
	- It contains a networking component (virtual ethernet) and a disk storage component (volumes). This are shared if more than one container is in a pod
	- Has a unique IP address and a set of ports
	- Containers inside a pod can communicate using the localhost network interface
- One can be created through the Google Cloud Console or a command provided in Google Cloud SDK

```bash
# Creating clusters
> gcloud container clusters create k1
# Running an image from a container registry into a pod
> kubectl run nginx --image=nginx:1.15.7
# See the running nginx pods
> kubectl get pods
# Connect a load balancer to a deployment and expose to the public
#   This creates a service (representation of load blanacing)
#   with a fixed IP address for the pods connected to a public IP
> kubectl expose deployments ninx --port=80 --type=LoadBalancer
# Shows service name, type, cluster-IP, External IP, port and time since creation
> kubectl get services
# Scaling a deployment
> kubectl scale nginx --replicas=3
# or autoscaling based on cpu usage,
# scale up when CPU usage hits 80% of capacity
> kubectl autoscale nginx --min=10 --max=15 --cpu=80
```

A **deployment** represents a group of replicas of the same pod. It keeps the pods running even if a node on which some of them run fails. It can be used to contain a component of an application or an entire application

A **service**, created when exposing a deployment of pods to the internet, groups a set of pods together and provides a stable endpoint for them. Ex. A public IP address managed by a network load balancer.

This is a recommended solution for exposing deployments between applications as it usually creates and destroys pods, having each pod an unique IP address that doesn't remain stable over time. An stable endpoint is then provided by a service.

### Kubernetes configuration file

```bash
# Starting point to get a file from current architecture
> kubectl get pods -l "app=nginx" -o yaml
```
Example configuration file
```yaml
apiVersion: v1
kind: Deployment
metadata:
	name: nginx
	labels:
		app: nginx
spec:
	replicas: 3
	selector:
		matchLabels:
			app: nginx 
	template:
		metadata:
			labels:
				app: nginx
		spec:
			containers:
			- name: nginx
			- 
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjkwODQ0NzAxLC0xNjQ3OTk0MTM3LDMyMj
MxMTU3LC00NzMyNjY3NzRdfQ==
-->