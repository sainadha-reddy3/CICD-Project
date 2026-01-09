CI/CD Kubernetes Deployment Project
Overview

This project demonstrates a complete CI/CD pipeline for deploying a containerized application to Kubernetes using GitHub Actions, Docker, and Kubernetes manifests.
It reflects a real-world DevOps workflow where GitHub acts as the source of truth and Kubernetes manages runtime operations.

Architecture
GitHub (Source Code)
        |
        |  (GitHub Actions - CI)
        v
Docker Image Build & Push
        |
        |  (CD)
        v
Kubernetes Deployment
        |
        v
Pods + Service + HPA

Tech Stack

Version Control: Git, GitHub

CI/CD: GitHub Actions

Containerization: Docker

Orchestration: Kubernetes (Minikube / GKE compatible)

Autoscaling: Horizontal Pod Autoscaler (HPA)

Configuration: ConfigMaps & Secrets


CI/CD Pipeline Flow
Continuous Integration (CI)

Triggered on every push to the main branch:

Checkout source code

Build Docker image

Tag image with commit SHA

Push image to Docker registry

Continuous Deployment (CD)

After successful CI:

Authenticate to Kubernetes cluster

Update Deployment image with new tag

Apply Kubernetes manifests

Kubernetes performs rolling update

Kubernetes Resources Used

Deployment

Manages application pods

Supports rolling updates

Service

Exposes application internally/externally

ConfigMap

Stores non-sensitive configuration

Secret

Stores sensitive data (e.g., passwords)

Horizontal Pod Autoscaler (HPA)

Automatically scales pods based on CPU usage

Autoscaling (HPA)

Minimum replicas: 2

Maximum replicas: 6

Scaling metric: CPU utilization

Target utilization: 70%

HPA relies on metrics-server and CPU requests defined in the Deployment.

How to Deploy Locally (Minikube)
Prerequisites

Docker

kubectl

Minikube

Git

Steps
minikube start
kubectl apply -f k8s/
kubectl get pods
kubectl get svc


Access the application using port-forward or NodePort (based on Service type).

GitHub Actions Secrets Required

Configure the following secrets in your GitHub repository:

Secret Name	Description
DOCKER_USERNAME	Docker registry username
DOCKER_PASSWORD	Docker registry password/token
KUBE_CONFIG	Base64-encoded kubeconfig file
Key DevOps Concepts Demonstrated

Infrastructure as Code (IaC)

CI vs CD separation

Immutable Docker images

Rolling deployments

Autoscaling with HPA

Secure secret management

Git-based delivery workflow
