# Microservices Kubernetes Deployment

## Application

This project deploys four Node.js microservices on Kubernetes using Minikube.

Services:

- User Service - 3000
- Product Service - 3001
- Order Service - 3002
- Gateway Service - 3003

## Prerequisites

- Docker
- Minikube
- kubectl
- WSL/Ubuntu

## Start Minikube

minikube start

## Configure Docker

eval $(minikube docker-env)

## Build Images

docker build -t user-service:1.0 ./Microservices/user-service
docker build -t product-service:1.0 ./Microservices/product-service
docker build -t order-service:1.0 ./Microservices/order-service
docker build -t gateway-service:1.0 ./Microservices/gateway-service

## Deployments

kubectl apply -f submission/deployments/

## Services

kubectl apply -f submission/services/

## Verify

kubectl get pods
kubectl get services
kubectl get deployments

## Testing

User:

kubectl port-forward service/user-service 3000:3000

curl http://localhost:3000/users

Product:

kubectl port-forward service/product-service 3001:3001

curl http://localhost:3001/products

Order:

kubectl port-forward service/order-service 3002:3002

curl http://localhost:3002/orders

Gateway:

kubectl port-forward service/gateway-service 3003:3003

curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

## Kubernetes Service Discovery

kubectl run test-client \
  --image=curlimages/curl:latest \
  --rm -it \
  --restart=Never \
  -- sh

curl http://user-service:3000/users
curl http://product-service:3001/products
curl http://order-service:3002/orders
curl http://gateway-service:3003/api/users

## Troubleshooting

Check pods:

kubectl get pods

Check pod details:

kubectl describe pod <pod-name>

Check logs:

kubectl logs <pod-name>

Check services:

kubectl get services

Check events:

kubectl get events --sort-by=.lastTimestamp
