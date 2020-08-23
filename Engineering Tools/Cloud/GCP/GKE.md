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
```ssh
# Images can be uploaded to Google Container Registry
> docker build -t py-server
> docker run -d py-server
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTA0ODYzNDgsMzIyMzExNTcsLTQ3Mz
I2Njc3NF19
-->