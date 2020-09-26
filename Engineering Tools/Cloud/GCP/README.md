# Google Cloud Platform

Content sections
- IAM
- Networking
- Storage

## Deployment: Infrastructure as a Code

It's better to define templates for infrastructure to follow a declarative strategy instead of an imperative (introducing each command per each desired action)

GCP uses **Deployment Manager** (Infrastructure management service) to let users work in this way. Works with a YAML template file or a python file.

```bash
# Create new deployments through a declarative file
> gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
# confirm status from deployments
> gcloud deplyment-manager deployments list
```


## Proactive monitoring

Monitoring lets you figure out whether the changes you made were good or bad.
It lets you respond with information rather than with panic. GCP works with Stackdriver for monitoring, logging and diagnostics.
	- Infrastructure platforms, VMs, containers, middleware and application tiers, logs, metrics and traces.
	- Core components
		- Monitoring. Checks endpoints of web apps and other internet accessible services. Uptime checks, alerts and use with notification tools.
			- Allows dashboard creation to visualize the state of an application
		- Logging. View logs from applications and filter and search on them. Define metrics, based on log contents into dashboards and alerts. 
			- Receives from BigQuery, Cloud Storage and Cloud Pub/Sub.
		- Trace. Sample latency of app engine applications and report Per-URL statistics
		- Error Reporting. tracks and groups the errors in your cloud applications. Notifies new errors. 
		- Debugging. Connects application production data to the source code. Lets inspect the state of the app at any code location in production. Works best when code is in Cloud Source repositories

**Preparing environment in Google Cloud**
```bash
# Copyright 2017 Google Inc.

#

# Licensed under the Apache License, Version 2.0 (the "License");

# you may not use this file except in compliance with the License.

# You may obtain a copy of the License at

#

# http://www.apache.org/licenses/LICENSE-2.0

#

# Unless required by applicable law or agreed to in writing, software

# distributed under the License is distributed on an "AS IS" BASIS,

# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.

# See the License for the specific language governing permissions and

# limitations under the License.

echo  "Creating App Engine app"

gcloud app create --region "us-central"

  

echo  "Making bucket: gs://$DEVSHELL_PROJECT_ID-media"

gsutil mb gs://$DEVSHELL_PROJECT_ID-media

  

echo  "Exporting GCLOUD_PROJECT and GCLOUD_BUCKET"

export GCLOUD_PROJECT=$DEVSHELL_PROJECT_ID

export GCLOUD_BUCKET=$DEVSHELL_PROJECT_ID-media

  

echo  "Installing dependencies"

npm install -g npm@6.11.3

npm update

  

echo  "Creating Datastore entities"

node setup/add_entities.js

  

echo  "Project ID: $DEVSHELL_PROJECT_ID"
```

**2nd example**

```bash
# Copyright 2017 Google Inc.

#

# Licensed under the Apache License, Version 2.0 (the "License");

# you may not use this file except in compliance with the License.

# You may obtain a copy of the License at

#

# http://www.apache.org/licenses/LICENSE-2.0

#

# Unless required by applicable law or agreed to in writing, software

# distributed under the License is distributed on an "AS IS" BASIS,

# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.

# See the License for the specific language governing permissions and

# limitations under the License.

echo  "Creating App Engine app"

gcloud app create --region "us-central"

  

echo  "Making bucket: gs://$DEVSHELL_PROJECT_ID-media"

gsutil mb gs://$DEVSHELL_PROJECT_ID-media

  

echo  "Exporting GCLOUD_PROJECT and GCLOUD_BUCKET"

export GCLOUD_PROJECT=$DEVSHELL_PROJECT_ID

export GCLOUD_BUCKET=$DEVSHELL_PROJECT_ID-media

  

echo  "Installing dependencies"

npm install -g npm@6.11.3

npm update

  

echo  "Creating Datastore entities"

node setup/add_entities.js

  

echo  "Creating Cloud Pub/Sub topic"

gcloud pubsub topics create feedback

  

echo  "Creating Cloud Spanner Instance, Database, and Table"

gcloud spanner instances create quiz-instance --config=regional-us-central1 --description="Quiz instance" --nodes=1

gcloud spanner databases create quiz-database --instance quiz-instance --ddl "CREATE TABLE Feedback ( feedbackId STRING(100) NOT NULL, email STRING(100), quiz STRING(20), feedback STRING(MAX), rating INT64, score FLOAT64, timestamp INT64 ) PRIMARY KEY (feedbackId);"

  

echo  "Project ID: $DEVSHELL_PROJECT_ID"
```

**Docker files: example using Cloud Build**

```bash
# Building docker images with cloud build 
gcloud builds submit -t gcr.io/$DEVSHELL_PROJECT_ID/quiz-frontend ./frontend/
# Create deployments from yaml file
kubectl create -f ./frontend-deployment.yaml
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwODQwNjY4MiwxOTcyNDIxNDQ5LC0xOD
ExMDA2Mjc4LDIwMTA0NTgsNDc1MDQyOTQ1LDEyNjEwMjg3NzEs
MTExNjA0MTU5NSwxMTcwNzUyNTgzLC01NDQyNDcxNTUsLTg1MT
UxMzY0OSw3NDUzOTg2ODBdfQ==
-->