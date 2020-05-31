
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

## Best practices for Dockerfiles

- Identify best base image to render a new image with required specifications (optimized, small, etc.)
- Only copy dependencies' file first to docker and install. This is to take advantage of build caches. Copy commands invalidate cache 
- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMTQ0MDYzNTAsMTgxNjE3OTU3M119
-->