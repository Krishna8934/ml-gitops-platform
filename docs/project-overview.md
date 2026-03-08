# Project Overview

## Introduction

The ML GitOps Automation Platform demonstrates a production-style DevOps workflow for deploying a machine learning API using modern cloud-native technologies.

The project showcases how automated CI pipelines, containerization, Kubernetes orchestration, GitOps deployment strategies, and monitoring systems can work together to create a reliable and scalable platform.

The system uses GitHub Actions for CI automation, Docker for containerization, Kubernetes for orchestration, ArgoCD for GitOps deployment, and Prometheus with Grafana for observability.

---

## Objectives

The primary objective of this project is to simulate a real-world DevOps environment and demonstrate the following capabilities:

- Automated CI/CD pipeline
- Containerized ML application deployment
- GitOps-based Kubernetes deployment
- Infrastructure monitoring and observability
- Production reliability features such as scaling and self-healing

---

## System Components

### The platform consists of multiple components working together:

#### ML Application

A FastAPI-based machine learning API that exposes endpoints for predictions, health checks, and metrics.

#### Containerization

The application is packaged into Docker images to ensure consistent execution across environments.

#### CI Pipeline

GitHub Actions automatically builds Docker images and updates Kubernetes manifests.

#### GitOps Deployment

ArgoCD monitors the manifest repository and synchronizes deployments with the Kubernetes cluster.

#### Monitoring

Prometheus collects application metrics while Grafana provides visualization dashboards.

---

## High Level Workflow

1. Developer pushes code to the GitHub repository
2. GitHub Actions builds a Docker image
3. The image is pushed to Docker Hub
4. Kubernetes manifests are updated with the new image tag
5. ArgoCD detects the change and deploys it to the cluster
6. Prometheus collects metrics from the application
7. Grafana visualizes system performance