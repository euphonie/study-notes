# Monitoring & Management

Reliable release process involves release and testing phases of software delivery. Main components for CI/CD pipelines.

**CI Pipeline**
- Pull from master
- Commit to feature branch
- Push to repository
	- Cloud Source
	- Github
- Build triggers in Jenkins, Circle CI, Github Actions, etc.
- Create image and store in artifact repository like Container registry
- Deployment manager like Spinnaker deploys the image
- Run test suites 
- If test are successful code can be promoted to a release branch

**CD Pipeline**
- It involves no manual stages
- The deployment system deploys the application images to the staging environment
- Runs integration tests, performance tests and more
- If tests are successful the image is tagged as a release candidate
- Approval of release candidate can trigger deployment to canary or blue-green production environments
- Monitor the performance of production using services like StackDriver
- If deployment works successfully entire traffic can be switched to the new release
- If there are any errors a rollback to the last stable release can be performed

##  Cloud Build
- Fully managed service
- Set up build pipelines to create a Docker container image and push the image to a Google Cloud resource
- Pipeline is automatically triggered by changes to the repository
	- Push to a branch, push of a tag, etc.
- Requires a build configuration file that specifies the steps of the pipeline
- Each step is a docker container executing the script indicated
	- Step name identifies the container image
	- Image attribute identifies the base image for the container
- Can be specified in YAML or JSON notation
- Source code is mounted to the /workspace directory
	- The artifacts are persisted in the directory
- Publishes build status notifications to Cloud Pub/Sub
- 

## Container Registry
- Registry for images uploaded to Google Cloud


## Deployment Manager
- Enables deployment of VM instances on container images that are created by the build pipeline


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk0MDMyNTcwLC0xNTYzMjUwNzg5LC0xND
Y2OTUxNDE1LC0xNjQwNDI1MTg2XX0=
-->