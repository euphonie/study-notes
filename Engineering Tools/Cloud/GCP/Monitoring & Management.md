# Monitoring & Management

Reliable release process involves release and testing phases of software delivery. Main components for CI/CD pipelines.

## CI pipeline
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

##  Cloud Build


## Container Registry


## Deployment Manager

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU4NzU3MDc0OCwtMTQ2Njk1MTQxNSwtMT
Y0MDQyNTE4Nl19
-->