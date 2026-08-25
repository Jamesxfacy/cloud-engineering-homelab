# CLOUD-001 — Kubernetes NGINX Deployment Fundamentals

## Overview

This project is the first lab in my Cloud Engineering Home Lab portfolio.

The goal was to build a foundational understanding of Kubernetes by deploying an NGINX web application and managing its lifecycle using Kubernetes manifests and `kubectl`.

The project covers application deployment, Pod management, Service networking, scaling, self-healing, logs, rolling updates, and deployment rollbacks.

---

## Architecture

```text
                 Local Browser
                      |
                localhost:8080
                      |
              kubectl port-forward
                      |
                NGINX Service
                      |
              +-------+-------+
              |               |
           NGINX Pod       NGINX Pod
              \               /
               \             /
                 Deployment
                      |
                  ReplicaSet
```

---

## Technologies

- Kubernetes
- Docker containers
- NGINX
- YAML
- kubectl
- PowerShell
- Git
- GitHub

---

## Project Structure

```text
CLOUD-001-nginx-deployment/
├── README.md
├── deployment.yaml
└── service.yaml
```

---

## Kubernetes Deployment

The application is defined using a Kubernetes Deployment.

The Deployment provides declarative management of the NGINX workload and allows Kubernetes to maintain the desired number of application replicas.

Key concepts practiced include:

- Deployments
- Pods
- ReplicaSets
- Labels
- Selectors
- Container images

---

## Service Networking

A Kubernetes Service provides a stable network endpoint for the NGINX Pods.

This allowed me to access the application without relying directly on individual Pod IP addresses.

The application was tested locally using Kubernetes port forwarding.

Example:

```bash
kubectl port-forward service/nginx-service 8080:80
```

---

## Scaling

I practiced scaling the Deployment to multiple replicas.

Example:

```bash
kubectl scale deployment nginx-deployment --replicas=3
```

Kubernetes automatically created additional Pods until the actual state matched the desired replica count.

This demonstrated Kubernetes' declarative reconciliation model.

---

## Self-Healing

I tested Kubernetes self-healing by manually deleting one of the running Pods.

Because the Deployment specified a desired replica count, Kubernetes automatically created a replacement Pod.

This demonstrated an important Kubernetes principle:

> Individual Pods are disposable. Controllers maintain the desired application state.

---

## Application Logs

I practiced retrieving container logs using:

```bash
kubectl logs <pod-name>
```

and following logs in real time using:

```bash
kubectl logs -f <pod-name>
```

Application logs are an important first step when investigating workload and container problems.

---

## Rolling Updates

I updated the container image managed by the Deployment and observed Kubernetes perform a rolling update.

This allowed the application version to change while Kubernetes progressively replaced existing Pods.

Useful commands included:

```bash
kubectl rollout status deployment/nginx-deployment
```

and:

```bash
kubectl rollout history deployment/nginx-deployment
```

---

## Deployment Rollback

I also practiced restoring a previous Deployment revision.

Example:

```bash
kubectl rollout undo deployment/nginx-deployment
```

After the rollback, I verified that the Deployment and Pods returned to the expected state.

---

## Useful Commands

```bash
# Cluster information
kubectl cluster-info

# Check nodes
kubectl get nodes

# List Pods
kubectl get pods

# Detailed Pod information
kubectl describe pod <pod-name>

# Application logs
kubectl logs <pod-name>

# Follow logs
kubectl logs -f <pod-name>

# Deployments
kubectl get deployments

# Services
kubectl get services

# Scale Deployment
kubectl scale deployment <deployment-name> --replicas=<number>

# Monitor rollout
kubectl rollout status deployment/<deployment-name>

# Rollout history
kubectl rollout history deployment/<deployment-name>

# Roll back Deployment
kubectl rollout undo deployment/<deployment-name>

# Port forwarding
kubectl port-forward service/<service-name> 8080:80
```

---

## Key Lessons

This project helped reinforce several core Kubernetes concepts:

- Kubernetes uses declarative configuration to maintain desired state.
- Deployments manage application Pods through ReplicaSets.
- Pods should generally be treated as replaceable resources.
- Services provide stable networking for dynamic Pods.
- Scaling can be performed without manually creating individual Pods.
- Kubernetes controllers provide application self-healing.
- Logs and `kubectl describe` are essential troubleshooting tools.
- Rolling updates allow workloads to be updated progressively.
- Deployment revisions can be rolled back when an update causes problems.
- Infrastructure configuration should be tracked with Git.

---

## Skills Demonstrated

- Kubernetes fundamentals
- YAML manifests
- NGINX deployment
- Pod lifecycle management
- ReplicaSets
- Kubernetes Services
- Scaling
- Self-healing
- Container logs
- Rolling updates
- Deployment rollbacks
- kubectl troubleshooting
- Git version control

---

## Status

**Completed**

This project is part of my ongoing Cloud Engineering Home Lab portfolio.