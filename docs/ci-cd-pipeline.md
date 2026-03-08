# CI/CD Pipeline

This document explains the Continuous Integration and GitOps-based deployment pipeline used in the **ML GitOps Automation Platform**.

The project implements a fully automated workflow that builds container images, updates Kubernetes manifests, and triggers deployment using GitOps principles.

---

## CI/CD Overview

The platform follows a **Git-driven CI/CD architecture** where every code change automatically triggers the build and deployment process.

Pipeline Flow:

Developer → GitHub → GitHub Actions → Docker Hub → Manifest Repository → ArgoCD → Kubernetes Cluster

---

##  Continuous Integration Pipeline

The CI pipeline is implemented using **GitHub Actions**.

Whenever code is pushed to the application repository, the CI workflow automatically starts and performs the following tasks.

---

## Step 1: Code Push

The pipeline begins when a developer pushes code to the GitHub repository.

Developer -> Git Push -> GitHub Repository

This push event triggers the GitHub Actions workflow.

---

## Step 2: GitHub Actions Workflow Trigger

GitHub Actions detects the push event and starts the CI pipeline defined inside:

.github/workflows/ci.yml

The workflow runs inside a GitHub-hosted runner environment.

---

## Step 3: Checkout Repository

The first step of the workflow checks out the repository code into the runner environment.

this allows the pipeline to access the project files including the Dockerfile.

## Step 4: Docker Image Build

The pipeline builds the Docker image for the FastAPI application. 

Example :
docker build -t username/ml-gitops-app:tag .

this step packages the application into a container image ready for deployment.

## Step 5: Push image to Docker Hub

after building the image, the pipeline pushes it to Docker Hub.

Example: 
docker push username/ml-gitops-app:tag

This allows Kubernetes to pull the image during deployment.

---

## Step 6: Update Kubernetes Manifest Repository

The CI pipeline automatically updates the **image tag inside the Kubernetes manifest repository**.

Example change in `deployment.yaml`.

### Before

image: username/ml-gitops-app:v1

### after 
image: username/ml-gitops-app:v2

this updated manifest is committed and pushed to the manifest repository.

## GitOps Deployment Trigger

Once the manifest repository is updated, the deployment process is automatically handled by ArgoCD.

ArgoCD continuously monitors the manifest repository. When a change is detected:

- ArgoCD identifies the new commit in the repository
- The Kubernetes cluster is synchronized with the updated manifests
- New containers are deployed automatically to the cluster

---

## Deployment Behavior

The Kubernetes deployment uses Rolling Updates to deploy new versions of the application.

This means:

- New pods are created with the updated container image
- Old pods are gradually terminated
- The application remains available during the update

This process enables zero-downtime deployments, ensuring that users experience no service interruption.

---

## Reliability Features

This CI/CD pipeline demonstrates several production-level reliability mechanisms:

### Automated Builds

Every code push automatically triggers the creation of a new container image.

### GitOps Deployment

All infrastructure and deployment changes are managed through Git commits, ensuring traceability.

### Rolling Updates

Application updates are deployed gradually without causing downtime.

### Self-Healing

If a pod fails, Kubernetes automatically recreates it, maintaining system stability.

### Version Control

Every deployment change is tracked in Git history, making it easy to roll back if necessary.

---

## Tools Used in the CI/CD Pipeline

Tool| Purpose
GitHub| Source code management
GitHub Actions| CI automation
Docker| Containerization
Docker Hub| Image registry
Kubernetes| Container orchestration
ArgoCD| GitOps deployment controller

---

## Complete Pipeline Summary

The complete GitOps-based CI/CD workflow of the platform is as follows:

1. Developer pushes code to GitHub
2. GitHub Actions CI pipeline starts automatically
3. A Docker image is built
4. The image is pushed to Docker Hub
5. The Kubernetes manifest repository is updated with the new image tag
6. ArgoCD detects changes in the repository
7. The Kubernetes cluster is synchronized
8. The new application version is deployed automatically

---

This workflow demonstrates a fully automated GitOps-based CI/CD system for deploying a machine learning API using modern DevOps practices.