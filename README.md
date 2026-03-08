# ML GitOps Automation Platform

A production-style DevOps pipeline demonstrating GitOps-based deployment of a FastAPI machine learning application using Docker, Kubernetes, ArgoCD, and automated CI/CD workflows with GitHub Actions. The platform includes automated image builds, GitOps deployments, observability with Prometheus and Grafana, and production-style reliability features such as rolling updates, scaling, and self-healing.

---

## Live Application

Live demo of the deployed application:

Live URL

https://ml-gitops-app.onrender.com

---

## GitHub Repositories

This project is organized into two repositories following GitOps principles.

Application Repository

Contains the FastAPI ML application, Dockerfile, and CI pipeline.

https://github.com/Krishna8934/ml-gitops-app

Manifest Repository

Contains Kubernetes manifests that ArgoCD continuously monitors and deploys.

https://github.com/Krishna8934/ml-gitops-manifests

---

## Technology Stack

FastAPI • Python • Docker • Kubernetes (Minikube) • GitHub Actions • ArgoCD • Prometheus • Grafana • Render

---

## Key Features

CI pipeline automatically builds Docker images ,
GitOps deployment using ArgoCD,
Rolling updates in Kubernetes,
Self-healing pods,
Horizontal scaling,
Prometheus metrics,
Grafana dashboards

---

## System Architecture

The platform demonstrates a complete GitOps-based DevOps pipeline for deploying a machine learning API.
The architecture integrates CI automation, containerization, Kubernetes orchestration, GitOps deployment, and monitoring.

architecture/complete automation flow.png

---

## CI/CD Pipeline

The project implements an automated CI pipeline using GitHub Actions.

Whenever a developer pushes code to the application repository, the CI workflow automatically performs the following steps:

1. Checkout the repository code
2. Build the Docker image for the FastAPI ML application
3. Push the Docker image to Docker Hub
4. Update the image tag inside the Kubernetes manifest repository
5. Commit the updated manifest back to GitHub

This automated pipeline ensures that every code change results in a new container image ready for deployment through GitOps.

---

## GitOps Deployment with ArgoCD

The platform follows GitOps principles for Kubernetes deployments.

ArgoCD continuously monitors the manifest repository containing Kubernetes deployment configurations. Whenever a change is detected in the repository, ArgoCD automatically synchronizes the Kubernetes cluster to match the desired state defined in Git.

This enables:

- Automated deployments
- Version-controlled infrastructure
- Easy rollback capability
- Transparent deployment history

---

## Kubernetes Deployment

The application runs inside a Kubernetes cluster using a Deployment and Service configuration.

Key capabilities include:

- Containerized ML API running inside Kubernetes Pods
- Service exposure using Kubernetes Service
- Rolling updates for zero-downtime deployments
- Replica-based scaling
- Self-healing through automatic pod recreation

---

## Observability & Monitoring

The platform includes a monitoring stack using Prometheus and Grafana.

Prometheus collects metrics from the FastAPI application and Kubernetes cluster, including:

- API request count
- Request latency
- CPU usage
- Memory usage

Grafana dashboards visualize these metrics in real time, enabling performance monitoring and debugging of the system.

---

## Production Simulation

To demonstrate production reliability, several real-world scenarios were tested:

- Scaling the application to multiple replicas
- Rolling updates with new container images
- Deleting running pods to verify self-healing
- Observing metrics during simulated traffic

These tests validate the resilience and automation capabilities of the platform.

---

## System Screenshots

This section demonstrates the working of the complete DevOps pipeline including CI automation, Kubernetes deployment, GitOps synchronization, monitoring, and production simulations.

### 1. GitHub Actions CI Pipeline

CI pipeline successfully building the application and triggering automated workflows.

![GitHub Actions CI](screenshots/ci-pipeline-success.png)

![GitHub Actions Build](screenshots/github-actions-build-success.png)

### 2. Docker Image Build

Docker image built successfully before deployment.

![Docker Images](screenshots/docker-image-built.png)

### 3. Kubernetes Deployment

Application deployed inside Kubernetes cluster.

![Kubernetes Service](screenshots/kubernetes-service-nodeport.png)

![Kubernetes Pods](screenshots/kubernetes-pods-running.png)


### 4. Kubernetes Self Healing

Demonstrating Kubernetes self-healing where deleted pods are automatically recreated.

![Kubernetes Self Healing](screenshots/kubectl-self-healing.png)

![Kubernetes Self Healing 2](screenshots/kubectl-self-healing2.png)


### 5. ArgoCD GitOps Deployment

ArgoCD automatically syncing the Kubernetes manifests from the Git repository.

![ArgoCD OutOfSync](screenshots/argocd-outofsync.png)

![ArgoCD Sync Success](screenshots/argocd-sync-success.png)

![ArgoCD Deployment Tree](screenshots/argo-cd-deployment-tree.png)


### 6. Prometheus Monitoring

Prometheus collecting application metrics and monitoring system targets.

![Prometheus Query](screenshots/prometheus-query-requests.png)

![FastAPI Metrics](screenshots/fastapi-metrics-endpoint.png)

![Prometheus Targets](screenshots/prometheus-targets.png)


### 7. CI Driven Image Updates

Automatic image updates through CI triggering GitOps deployment.

![ArgoCD Image Update](screenshots/argocd-image-version-update.png)

![CI Image Update](screenshots/argocd-ci-image-update.png)


### 8. GitOps Monitoring Integration

Prometheus monitoring integrated into the GitOps deployment pipeline.

![ArgoCD Monitoring](screenshots/argocd-prometheus-monitoring.png)


 ### 9. Resource Management & Scaling

Demonstrating Kubernetes resource limits and scaling capabilities.

![Resource Limits](screenshots/argocd-resource-limits-update.png)

![Scaled Deployment](screenshots/argocd-scaled-deployment.png)


### 10. Grafana Dashboards

Grafana dashboards visualizing cluster performance and request metrics.

![Grafana Cluster](screenshots/grafana-cluster-dashboard.png)

![Grafana Node Monitoring](screenshots/grafana-node-monitoring.png)

![Grafana Request Metrics](screenshots/grafana-request-metrics.png)

![Grafana Prometheus Query](screenshots/grafana-prometheus-query-png.png)

![Grafana Request Rate](screenshots/grafan-prometheus-requests-rate.png)

---

## Author

Name: Krishna Mishra

LinkedIn: https://www.linkedin.com/in/krishna-mishra-cse/

GitHub: https://github.com/Krishna8934  