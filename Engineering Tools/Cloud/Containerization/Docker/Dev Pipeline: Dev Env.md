
# About
Using docker to build dev environments to streamline process of modifying codebases.

> Notes created from content in **DockerCon 2020's presentation by Ancha Lordache's Best Practices for Compose-managed Python Applications** 
> [on Youtube](https://www.youtube.com/watch?v=OkidaZmnADw&feature=youtu.be)

# Requisites 
- Docker desktop on environment

# Key points

## Containerize application

A project's should follow the structure: 

Project
|__ app
|_____ Dockerfile
|_____ <dependencies' file>
|_____ <project's src>
|__ docker-compose.yaml

## Best practices for Dockerfiles

- Identify best base image to render a new image with required specifications (optimized, small, etc.)
- Only copy dependencies' file first to docker and install. This is to take advantage of build caches.
- Layers that don't update frequently should be added before layers that do change to optimize caching mechanisms.
- inside docker-composer services section expose required services with ports section as follow: 
```yaml
version: 3.7
services:
    db:
	    image: mysql:8.0.19
	    restart:always
	    environment:
	    - MYSQL_DATABSE=example
	    - MYSQL_ROOT_PASSWORD=pass
	app:
		build:app
		restart: always
		ports:
		- 5000:5000
	web: 
		build: web
		restart:always
		ports:
		- 80:80
```
- Network isolation for multiple services can be defined in docker-compose
```yaml
db: 
	...
	networks:
	- backend-network
app:
	...
	networks:
	- backend-network
	- frontend-network
web:
	...
	networks:
	-frontend-network

networks:
	- backend-network
	- frontend-network
```
- To persist data a volume needs to be defined. And secrets can be shared securely to services using the secrets section
```yaml
db: 
	...
	networks:
	- backend-network
	volumes:
	- db-data: /var/lib/mysql
	secrets:
	- db-password
...
volumes:
	db-data:
secrets:
	db-password:
		
```
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk0ODU0OTc4NSwtMTcyNjQ3Njg0OSw4MT
YwNjk5MzIsMTgxNjE3OTU3M119
-->