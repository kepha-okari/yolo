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

verify if images were created and pushed successfully with
git status
`gcloud container images list --repository=gcr.io/my-project`

### STEP 3: Create a GKE Cluster

- Go to the [GKE console](https://console.cloud.google.com/) and click "Create cluster"
- Choose a name for your cluster, select the desired zone/region, and choose the appropriate number of nodes and machine type
- Under "Networking," select "Default" or create a new network and subnetwork
- Click "Create" to create the cluster

### STEP 4: Deploy

Create a Kubernetes deployment for each app by running
`kubectl create deployment` command for each deployment, specifying the name of the deployment, the name and tag of the Docker image, and any necessary environment variables or configuration options.
Example, for backend app do: `kubectl create deployment backend --image=gcr.io/[PROJECT-ID]/[BACKEND-IMAGE-NAME]:[TAG] --env MONGO_URI=[MONGO_URI]`

for client app do: `kubectl create deployment backend --image=gcr.io/[PROJECT-ID]/[CLIENT-IMAGE-NAME]:[TAG] --env MONGO_URI=[MONGO_URI]`

- Create a Kubernetes deployment file (e.g., a YAML file) that describes your app
- The deployment file should specify the container image for your app, the desired number of replicas, and any necessary environment variables, volumes, or ports
- Use kubectl to apply the deployment file to your cluster, using a command like: kubectl apply -f <filename>
- Verify that your deployment was successful by running `kubectl get deployments` and `kubectl get pods`

### STEP 5: Create Services

Create a Kubernetes service for each app by running kubectl expose deployment command for each service, specifying the name of the service, the port to expose, and any necessary configuration options. For example, to create a service for the backend app, you can run:

### STEP 6: Expose App

`kubectl expose deployment backend --port=5000 --target-port=5000 --type=LoadBalancer`
Similarly, to create a service for the client app, you can run:

`kubectl expose deployment client --port=3000 --target-port=3000 --type=LoadBalancer`

### STEP 6: Access App

Access your deployed client app by finding the external IP address of the client app service, which you can do by running `kubectl get services`. Once you have the external IP address, you can access your client app by visiting the address in your web browser.
