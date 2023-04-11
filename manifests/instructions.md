### STEP 1: Authenticate Docker client to GCR using CLI

Authenticate your Docker client to GCR using the command below. Replace [PROJECT-ID] with your GCP project ID.

`gcloud auth configure-docker --project=[PROJECT-ID]`

Build the Docker images for your backend and client apps by running docker build command for each image

### STEP 2: Build and push Images to GCR (goggle container registry)

#### Backend Image

`cd path/to/client/Dockerfile`

`docker build -t gcr.io/[PROJECT-ID]/[BACKEND-IMAGE-NAME]:[TAG] .`

Push the built Docker images to your Google Container Registry by running docker push command for each image. For example, to push the backend app image, you can run:

`docker push gcr.io/[PROJECT-ID]/[BACKEND-IMAGE-NAME]:[TAG]`

#### Client Image

`cd path/to/client/Dockerfile`

`docker build -t gcr.io/[PROJECT-ID]/[CLIENT-IMAGE-NAME]:[TAG] .`

Push the built Docker images to your Google Container Registry by running docker push command for each image. For example, to push the backend app image, you can run:

`docker push gcr.io/[PROJECT-ID]/[CLIENT-IMAGE-NAME]:[TAG]`

### STEP 2: Create a GKE Cluster

- Go to the [GKE console](https://console.cloud.google.com/) and click "Create cluster"
- Choose a name for your cluster, select the desired zone/region, and choose the appropriate number of nodes and machine type
- Under "Networking," select "Default" or create a new network and subnetwork
- Click "Create" to create the cluster

docker push gcr.io/[PROJECT_ID]/client:v1
Create a Kubernetes deployment for each app by running kubectl create deployment command for each deployment, specifying the name of the deployment, the name and tag of the Docker image, and any necessary environment variables or configuration options. For example, to create a deployment for the backend app, you can run:

kubectl create deployment backend --image=gcr.io/[PROJECT_ID]/backend:v1 --env MONGO_URI=[MONGO_URI]
Replace [PROJECT_ID] with your GCP project ID, and [MONGO_URI] with the URI of your MongoDB instance.

Similarly, to create a deployment for the client app, you can run:

kubectl create deployment client --image=gcr.io/[PROJECT_ID]/client:v1 --env REACT_APP_API_URL=[BACKEND_SERVICE_URL]
Replace [PROJECT_ID] with your GCP project ID, and [BACKEND_SERVICE_URL] with the URL of the backend app service, which will be created in the next step.

Create a Kubernetes service for each app by running kubectl expose deployment command for each service, specifying the name of the service, the port to expose, and any necessary configuration options. For example, to create a service for the backend app, you can run:

kubectl expose deployment backend --port=5000 --target-port=5000 --type=LoadBalancer
Similarly, to create a service for the client app, you can run:

kubectl expose deployment client --port=3000 --target-port=3000 --type=LoadBalancer
Access your deployed client app by finding the external IP address of the client app service, which you can do by running kubectl get services. Once you have the external IP address, you can access your client app by visiting the address in your web browser.
