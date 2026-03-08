# Kubernetes Deployment

This document explains how the FastAPI ML application is deployed inside a Kubernetes cluster.

The project uses **Minikube** as the local Kubernetes environment and deploys the application using **Kubernetes Deployment and Service resources**.

---

# Kubernetes Environment

The application is deployed inside a Kubernetes cluster created using **Minikube**.

Minikube provides a local Kubernetes environment suitable for development and testing.

Cluster components used in this project:

- Kubernetes API Server
- Worker node (Minikube VM / container)
- Kubernetes scheduler
- Kubernetes controller manager

The cluster manages containerized workloads and ensures that the application remains available.

---

# Application Container

Before deploying to Kubernetes, the FastAPI application is containerized using Docker.

The Docker image contains:

- FastAPI ML application
- Python dependencies
- Prometheus metrics endpoint
- Uvicorn server

Docker image example: krishna23243/ml-gitops-app:latest

This image is stored in **Docker Hub** so Kubernetes can pull it during deployment.

---

# Kubernetes Deployment Resource

The application runs inside Kubernetes using a **Deployment** resource.

A Deployment manages application pods and ensures that the desired number of replicas are always running.

Example deployment configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-app
  template:
    metadata:
      labels:
        app: ml-app
    spec:
      containers:
      - name: ml-app-container
        image: krishna23243/ml-gitops-app:latest
        ports:
        - containerPort: 8000
```
### Deployment Responsibilities
The Kubernetes Deployment performs several
important tasks:
• Creates application pods
• Maintains the desired replica count
• Performs rolling updates
• Enables self-healing
• Manages pod lifecycle

## Kubernetes Service
To expose the application externally, a
Kubernetes Service is used.
The project uses a NodePort service.

Example configuration:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: ml-app-service
spec:
  type: NodePort
  selector:
    app: ml-app
  ports:
    - port: 80
      targetPort: 8000
      nodePort: 30007
```

### Service Responsibilities
The Kubernetes Service provides:
• Stable networking for pods
• Load balancing across replicas
• External access to the application

Traffic flow:
User → NodePort → Kubernetes Service → Pods

## Scaling the Application
The deployment supports horizontal scaling
Scaling is performed by increasing the number
of replicas in the deployment.

Example:
```yaml
replicas: 3
```

Kubernetes then creates multiple pods running
the same application.
Benefits:
• Increased availability
• Load distribution
• Fault tolerance

## Rolling Updates
Kubernetes Deployments support rolling
updates.
During an update:
1. New pods are created with the updated
container image
2. Old pods are gradually terminated
3. Traffic is routed only to healthy pods

This ensures:
• Zero downtime deployments
• Safe updates
• Automatic rollback capability

## Self Healing
Kubernetes automatically ensures that the
desired number of pods remain running.
If a pod fails:
• Kubernetes detects the failure
• The failed pod is terminated
• A new pod is created automatically
This guarantees application reliability.

## Deployment Verification
The deployment status can be verified using
Kubernetes commands.
Check running pods:
```yaml
kubectl get pods
```
Check services:
```yaml
kubectl get svc
```

Describe deployment:
```yaml
kubectl describe deployment
ml-app-deployment

```
These commands help monitor the application
state in the cluster.

## Kubernetes Deployment Summary
The Kubernetes deployment provides the
following capabilities:
• Container orchestration
• Automated pod management
• Horizontal scaling
• Rolling updates
• Self-healing infrastructure
• Service-based networking

This setup ensures that the ML application runs
reliably inside a Kubernetes cluster and can
handle production-style workloads.