# Spring Boot Microservices
This is a personal project where I’ve been experimenting with building a robust microservices architecture using a variety of modern technologies.

## Microservices Overview
This project is composed of several microservices, each designed to handle a specific part of the application’s domain:
- Product Service: Manages product details and inventory levels.
- Order Service: Handles customer orders, including order creation, status tracking, and payment processing.
- Inventory Service: Keeps track of inventory levels, ensuring that orders are only placed if the items are in stock.
- Notification Service: Sends notifications to customers, whether it’s order confirmations, shipping updates, or any other event.
- API Gateway: The single entry point for all clients, handling requests and routing them to the appropriate services


## Tech Stack

I’ve used a bunch of technologies that I’m particularly interested in. Here’s what powers this project:

- Spring Boot: The backbone of the microservices, providing all the essential features for building robust and scalable applications.
- Mongo DB: Handling data storage for some of the services, especially where flexibility and scalability are crucial.
- MySQL: For relational data storage, mainly used by the Inventory Service.
- Kafka: Messaging between services, ensuring that communication is efficient and resilient.
- Keycloak: Managing authentication and authorization, centralizing the security aspects of the system.
- Test Containers with Wiremock:  For testing, allowing me to simulate different environments and ensure the services work as expected.
- Grafana Stack: Monitoring the whole system, with Prometheus for metrics, Loki for logs, and Tempo for tracing. It’s all about keeping an eye on the health of the microservices.
- Resilience4j: Implementing the circuit breaker pattern to handle faults gracefully and maintain system stability.
- Kubernetes: For orchestrating the deployment of services, managing the complexity of distributed systems, and ensuring everything runs smoothly.


## Application Architecture
![image](https://github.com/user-attachments/assets/d4ef38bd-8ae5-4cc7-9ac5-7a8e5ec3c969)

## For the frontend

Make sure you have the following installed on your machine:

- Node.js
- NPM
- Angular CLI

Run the following commands to start the frontend application

```shell
cd frontend
npm install
npm run start
```
## Building the backend services

Run the following command to build and package the backend services into a docker container

```shell
mvn spring-boot:build-image -DdockerPassword=<your-docker-account-password>
```

The above command will build and package the services into a docker container and push it to your docker hub account.

## For the backend services

Make sure you have the following installed on your machine:

- Java 21
- Docker
- Kind Cluster - https://kind.sigs.k8s.io/docs/user/quick-start/#installation

### Start Kind Cluster

Run the k8s/kind/create-kind-cluster.sh script to create the kind Kubernetes cluster

```shell
./k8s/kind/create-kind-cluster.sh
```
This will create a kind cluster and preload all the required docker images into the cluster, this will save you time downloading the images when you deploy the application.

### Deploy the infrastructure

Run the k8s/manisfests/infrastructure.yaml file to deploy the infrastructure

```shell
kubectl apply -f k8s/manifests/infrastructure.yaml
```

### Deploy the services

Run the k8s/manifests/applications.yaml file to deploy the services

```shell
kubectl apply -f k8s/manifests/applications.yaml
```

### Access the API Gateway

To access the API Gateway, you need to port-forward the gateway service to your local machine

```shell
kubectl port-forward svc/gateway-service 9000:9000
```

### Access the Keycloak Admin Console
To access the Keycloak admin console, you need to port-forward the keycloak service to your local machine

```shell
kubectl port-forward svc/keycloak 8080:8080
```

### Access the Grafana Dashboards
To access the Grafana dashboards, you need to port-forward the grafana service to your local machine

```shell
kubectl port-forward svc/grafana 3000:3000
```