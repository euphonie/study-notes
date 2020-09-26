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

## Container Registry
- Registry for images uploaded to Google Cloud


## Deployment Manager

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM5MTUyOTYzOSwtMTU2MzI1MDc4OSwtMT
Q2Njk1MTQxNSwtMTY0MDQyNTE4Nl19
-->