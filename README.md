# Kubernetes Deployment with PostgreSQL StatefulSet
This repository contains Kubernetes YAML configurations to deploy a sample application with a PostgreSQL database using a StatefulSet. The setup can be run on any local Kubernetes cluster like Minikube or K3d.

**Prerequisites**
Kubernetes cluster (Minikube, K3d, or similar)

kubectl configured to access your cluster

(Optional) Ingress controller installed (nginx, traefik, etc.)

(Optional) Service mesh (Istio, Linkerd, etc.) if you plan to use one

**Deployment Structure**
The deployment consists of:

A StatefulSet for PostgreSQL with persistent storage

A sample application deployment

Services for both components

(Optional) Ingress resource for external access

**Files**
postgres-statefulset.yaml: PostgreSQL StatefulSet with persistent volume claim

postgres-service.yaml: Headless service for PostgreSQL

app-deployment.yaml: Sample application deployment

app-service.yaml: Service for the application

ingress.yaml: (Optional) Ingress configuration

# Deployment Steps
Start your local Kubernetes cluster:

bash
minikube start

k3d cluster create mycluster

# Deploy PostgreSQL:

bash
kubectl apply -f postgres-statefulset.yaml
kubectl apply -f postgres-service.yaml

# Deploy the application:

bash
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
# (Optional) Deploy Ingress:

bash
kubectl apply -f ingress.yaml
# Verify the deployment:

bash
kubectl get all
kubectl get pvc
kubectl get pods

# Accessing the Application
For ClusterIP service:

bash
kubectl port-forward service/app-service 8080:80
Then access at http://localhost:8080

For NodePort service:

bash
minikube service app-service
For Ingress:

bash
minikube addons enable ingress
Then access using the hostname defined in the ingress resource

# Customization
Update the database credentials in postgres-statefulset.yaml

Modify the application image in app-deployment.yaml

Adjust resource requests/limits as needed

Update ingress host rules if using custom domains

Cleanup
To remove all resources:

bash
kubectl delete -f .
