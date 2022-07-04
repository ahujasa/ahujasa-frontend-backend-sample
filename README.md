# DevOps-Sample

In this repo, you will find a simple Python - Flask Web App, which reads the current RAM and CPU usage and a React frontend which shows the statistics in the browser.

![](./img/readme.jpg)

## How to run?

The app is setup in a pretty standard way, just like most Python-React Apps.

### Python Backend
In the api directory, do the following. 
1. `pip install -r requirements.txt`
2. `python app.py`
3. Visit `http://localhost:8000/stats`


### React Frontend
In the sys-stats directory, do the following.
1. `npm install`
2. `npm start`

## Task 1 - Dockerize the Application

1. api/Dockerfile-
   - This create Docker container by installing requirements.txt and then running app.py while exposing on port 8000. :8000/stats reference is expected to resolve to flask app. We call it "server" in docker-compose.yml file
2. sys-stats/Dockerfile-
  - This create Docker container by installing npm dependencies, then `npm run build` on each run. Finally exposes frontend 
    on port 3000 thru `npm run start`. We call it "client" in docker-compose.yml file later.
3. nginx/Dockerfile-
   - This create Docker container to reverse proxy client & server over port 9000. Default 9000 in client configuration of default.nginx points to "server" over port 3000. "/api" in default.nginx points to "client" over port 8000.
   So,in nutshell, when we run `docker-compose up --build` command, then it brings up react application over port http://localhost:9000 and http://localhost:9000/stats/api resolves to client flask application. 


## Task 2 - Deploy on Cloud

Next step is to deploy this application to absolutely any cloud of your choice. 

> It's important to remember here that the application is already containerize, maybe you could deploy it to services which take an advantage of that fact. (example, AWS EBS?)

You could use any other cloud service provider of your choice too. Use the smallest instance size available to save up on the cloud costs. 

The React App should be accessible on a public URL, that's the only hard requirement. 

Use the best practices for exposing the cloud VM to the internet, block access to unused ports, add a static IP (elastic IP for AWS), create proper IAM users and configure the app exactly how you would in production. Write a small document to explain your approach.

You will be evaluated based on the

* best practices
* quality of the documentation provided with the code

### Task 3 - Get it to work with Kubernetes

Next step is completely separate from step 2. Go back to the application you built in Stage 1 and get it to work with Kubernetes.

Separate out the two containers into separate pods, communicate between the two containers, add a load balancer (or equivalent), expose the final App over port 80 to the final user (and any other tertiary tasks you might need to do)

Add all the deployments, services and volume (if any) yaml files in the repo.

The only hard-requirement is to get the app to work with `minikube`


# frontend-backend-sample
