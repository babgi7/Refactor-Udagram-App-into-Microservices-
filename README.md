# Refactor-Udagram-App-into-Microservices-
#### Steps to build docker images:
before you run this project you need to install docker and Nodejs. After that naviagte to the follwoing folders

```sh
udacity-c3-restapi-user/
```

```sh
udacity-c3-restapi-feed/
```

```sh
udacity-c3-frontend/
```

```sh
udacity-c3-deployment/dokcer/
```

- build your docker images by running

```sh
docker build -t ${DOCKER USER NAME}/${IMAGE NAME} .
```
- push the image to docker hub

```sh
docker push ${DOCKER USER NAME}/${IMAGE NAME}
```
- After you do that with all 4 folders, Please go to  

```sh
udacity-c3-deployment/dokcer/
```

- change the images key at docker-composed.yaml.

- before you run the app please set the follwoing environment variables in you terminal  
```sh
POSTGRESS_USERNAME=XX
POSTGRESS_PASSWORD=XX
POSTGRESS_DB=postgres
POSTGRESS_HOST=XX
JWT_SECRET=XX
AWS_BUCKET=XX
AWS_PROFILE=XX
AWS_REGION=XX
AWS_ACCESS_KEY_ID=XX
AWS_SECRET_ACCESS_KEY=XX
aws_access_key_id=XX
aws_secret_access_key=XX
```

- finally that run

```sh
docker-compose up
```

Now open in your broswer
```sh
http://localhost:8100/
```
#### Steps to build cluster in aws:

run 
```sh
eksctl create cluster --name ${CLUSTER NAME} --version 1.14 --region ${REGION} --nodegroup-name standard-workers --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --node-ami auto
```
it will take some time to create cluster, meanwhile make sure to change yaml file at

```sh
udacity-c3-deployment/k8/
```

after that run this one by one
```sh
kubectl apply -f env-configmap.yaml
kubectl apply -f env-secret.yaml
kubectl apply -f backend-feed-deployment.yaml
kubectl apply -f backend-feed-service.yaml
kubectl apply -f backend-user-deployment.yaml
kubectl apply -f backend-user-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
kubectl apply -f reverseproxy-deployment.yaml
kubectl apply -f reverseproxy-service.yaml

```
