# k8s-pathbased_routing
Project for host a microservice based application in kubernetes cluster using pathbaed routing.

#### Assesment 1:

 - Step 1: Make sure your docker is running and start minikube cluster.

 - Step 2: Build the images of ms1, ms2, ms3

 - Step 3: Push these images on dockerhub / ecr

 - Step 4: Write ms1-deployment.yml describing the deployment of ms1.

 - Step 5: Write ms1-service.yml describing the service of ms1.

 - Step 6: Replicate these for all the other ms.

 - Step 7: Writing the ingress controller.


# Sample Microservice App in NodeJs

Note: This app is only for practicing various topics in DevOps and is not intended to create any application.

Create  `microservice1/.env` file with the content (replace value of `URL` with your own value):
```js
URL='http://192.168.0.104'
```

Build Process:

```sh
docker-compose build
```

## Docker Swarm

Set Up Docker Swarm:
```sh
docker swarm init
```

Deploy Service:

```sh
docker stack deploy -c docker-compose.yml microservice
```

Scaling:
```sh
docker service scale microservice_ms1=5
docker service scale microservice_ms2=2
docker service scale microservice_ms3=3
```
This will create microservice_ms1 with 5 replica, microservice_ms2 with 2 replica and microservice_ms3 with 3 replica.

Updating:
```sh
docker stack deploy -c docker-compose.yml microservice
```

Managing Service:

```sh
docker stack ps microservice
docker service ps microservice_ms3
```

Remove Services and Swarm:
```sh
docker stack rm microservice
```

To leave swarm:
```sh
docker swarm leave --force
```

## Building Image and Pushing into dockerhub

Build images inside mivroservices folder
```sh
cd microservice1
docker build -t kinnar0112/ms1:1.0 .

cd ../microservice2
docker build -t kinnar0112/ms2:1.0 .

cd ../microservice3
docker build -t kinnar0112/ms3:1.0 .
```

Pushing image to dockerhub
```sh
docker push kinnar0112/ms1:1.0
docker push kinnar0112/ms2:1.0
docker push kinnar0112/ms3:1.0
```

## Sample Commands for K8s

Start Minikube
```sh
minikube start
```

Apply Deployment And Services
```sh
cd k8s
kubectl apply -f ms1-deployment.yml
kubectl apply -f ms1-service.yml
kubectl apply -f ms2-deployment.yml
kubectl apply -f ms2-service.yml
kubectl apply -f ms3-deployment.yml
kubectl apply -f ms3-service.yml
```

Verify Deployment
```sh
kubectl get deployments
```

Verify Services
```sh
kubectl get services
```

Verify Pods
```sh
kubectl get pods
```