# GitOps Workflow

This document explains how **GitOps is implemented in the ML GitOps Automation Platform** using **ArgoCD and Kubernetes**.

GitOps is a deployment methodology where **Git repositories act as the single source of truth** for infrastructure and application deployments.

Instead of manually deploying applications to Kubernetes, the cluster automatically synchronizes with the configuration stored in Git.

---

# What is GitOps?

GitOps is a modern DevOps practice where:

- Infrastructure and deployments are defined as code
- All changes are made through Git commits
- Deployment systems automatically apply those changes to the cluster

Key principle:

**Git = Source of Truth**

This ensures that the Kubernetes cluster always matches the configuration defined in the Git repository.

---

# Repositories Used in the Project

The platform follows a **two-repository architecture**.

## Application Repository

ml-gitops-app

Contains:

- FastAPI ML application code
- Dockerfile
- GitHub Actions CI pipeline

Repository link: https://github.com/Krishna8934/ml-gitops-app

## Manifest Repository

ml-gitops-manifests

Contains:

- Kubernetes Deployment manifests
- Service configuration
- Monitoring configuration

Repository link: https://github.com/Krishna8934/ml-gitops-manifests

ArgoCD continuously monitors this repository.

---

# GitOps Deployment Flow

The deployment process follows this automated workflow.

### Step 1 — Developer Pushes Code

A developer updates the application and pushes code to the application repository.

Developer-> Git Push -> GitHub

---

### Step 2 — CI Pipeline Builds Container Image

GitHub Actions automatically:

1. Builds the Docker image
2. Pushes the image to Docker Hub
3. Updates the Kubernetes manifest repository with the new image tag

Example image update:

image: username/ml-gitops-app:v2

### Step 3 — Manifest Repository is Updated

The Cl pipeline commits the updated deployment configuration to the manifest repository.
This repository stores the desired state of the
Kubernetes cluster.

### Step 4 — ArgoCD Detects Changes
ArgoCD continuously monitors the manifest
repository.

When a new commit appears:
• ArgoCD detects the change
• The application status becomes OutOfSync


### Step 5 — ArgoCD Synchronizes the Cluster
ArgoCD automatically synchronizes the
Kubernetes cluster with the manifest repository.

During synchronization:
• New container images are deployed
• Kubernetes resources are updated
• The cluster state matches the Git repository

### Step 6 — Application is Updated in Kubernetes
Kubernetes performs a rolling update.
This means:
• New pods are created with the updated image
• Old pods are gradually terminated
• The application remains available during deployment
This ensures zero downtime updates.

## GitOps Benefits Demonstrated
The project demonstrates several advantages of
GitOps.
### Version Controlled Infrastructure
All deployment configurations are stored in Git.

### Automated Deployments
Application updates are deployed automatically
when manifests change.

### Easy Rollbacks
If a deployment fails, reverting to a previous Git
commit restores the previous system state.

### Transparent Deployment History
Every infrastructure change is recorded in Git
history.

## ArgoCD Application Monitoring
ArgoCD provides a visual interface showing:
• Application health
• Synchronization status
• Deployment tree
• pod status

Common states:

Status             Meaning
Healthy            Application running correctly
OutOfSync          Cluster differs from Git configuration
Synced             Cluster matches Git configuration 

## GitOps Workflow Summary
The complete GitOps workflow is:
1. Developer pushes code to GitHub

2. Cl pipeline builds Docker image

3. Image is pushed to Docker Hub

4. Kubernetes manifest repository is updated

5. ArgoCD detects the change

6. Kubernetes cluster is synchronized

7. Application is deployed automatically

This approach ensures a fully automated,
Git-driven deployment system for the machine
learning API.