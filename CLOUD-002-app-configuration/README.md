# CLOUD-002 — Kubernetes Application Configuration & Health Management

## Overview

This project builds on my introductory Kubernetes deployment lab by implementing application configuration management, secret handling, resource controls, health checks, service networking, and troubleshooting.

The application is deployed into a dedicated `development` namespace using a two-replica NGINX Deployment.

The project also includes a simulated incident in which an incorrect readiness probe causes new Pods to remain Running but Not Ready. The issue is investigated using Kubernetes status, events, Pod inspection, Service endpoints, and rollout information before the configuration is corrected and application health is verified.

---

## Architecture

```text
                    Local Browser
                         |
                    localhost:8080
                         |
                 kubectl port-forward
                         |
                  app-web-service
                    ClusterIP
                         |
               +---------+---------+
               |                   |
            app-web              app-web
             Pod 1                Pod 2
               |                   |
               +---------+---------+
                         |
                    Deployment
                    /         \
                   /           \
             ConfigMap        Secret
             app-config      app-secret
```

---

## Technologies

- Kubernetes
- Docker containers
- NGINX
- Git
- GitHub
- PowerShell
- YAML

---

## Kubernetes Resources

This project creates:

- Development Namespace
- ConfigMap
- Kubernetes Secret
- Deployment
- ReplicaSet
- Two application Pods
- ClusterIP Service
- Readiness Probe
- Liveness Probe
- CPU and memory requests
- CPU and memory limits

---

## Project Structure

```text
CLOUD-002-app-configuration/
├── README.md
├── namespace.yaml
├── configmap.yaml
├── secret.yaml.example
├── deployment.yaml
└── service.yaml
```

The real `secret.yaml` file is intentionally excluded from Git.

---

## Configuration Management

Non-sensitive application configuration is stored in a ConfigMap.

Example values include:

```text
APP_ENV
APP_MESSAGE
```

Sensitive configuration is stored separately using a Kubernetes Secret.

The application consumes both resources as environment variables through the Deployment.

---

## Secret Management

The real Kubernetes Secret manifest is maintained locally and excluded from version control using `.gitignore`.

A sanitized:

```text
secret.yaml.example
```

is included in the repository to document the expected Secret structure without exposing credential values.

> Base64 encoding should not be considered encryption. Production Kubernetes Secret management requires appropriate access controls and may require encryption at rest or an external secrets-management solution.

---

## Resource Management

The NGINX container defines CPU and memory requests and limits.

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "64Mi"
  limits:
    cpu: "250m"
    memory: "128Mi"
```

Requests provide Kubernetes with information used during scheduling, while limits constrain container resource consumption.

---

## Application Health Checks

The Deployment implements both readiness and liveness probes.

### Readiness Probe

The readiness probe determines whether the application is ready to receive traffic.

### Liveness Probe

The liveness probe helps Kubernetes determine whether the application container remains healthy or should be restarted.

---

## Troubleshooting Scenario

A simulated incident was introduced by changing the readiness probe from:

```text
/
```

to a nonexistent application path.

The updated containers started successfully, but the affected Pods remained:

```text
0/1 Running
```

This demonstrated an important Kubernetes concept:

> A Running container does not necessarily mean a Ready application.

---

## Troubleshooting Workflow

The incident was investigated using:

```bash
kubectl get pods -n development
kubectl describe pod <pod-name> -n development
kubectl get events -n development --sort-by=.metadata.creationTimestamp
kubectl get endpoints app-web-service -n development
kubectl describe service app-web-service -n development
kubectl rollout status deployment/app-web -n development
```

Pod events revealed that the readiness probe was failing.

The incorrect probe path was identified as the root cause.

---

## Resolution

The readiness probe path was restored to:

```text
/
```

The corrected Deployment was reapplied and Kubernetes successfully completed the rollout.

Recovery was verified by confirming:

- Both Pods were `1/1 Ready`
- Deployment reported `2/2` ready replicas
- Service endpoints were populated
- The application loaded through the Service
- HTTP testing returned `200 OK`

---

## Key Lessons

This project reinforced several important Kubernetes concepts:

- Separate application configuration from container images.
- Use ConfigMaps for non-sensitive configuration.
- Handle sensitive configuration separately using Secrets.
- Do not commit credential-containing manifests to public repositories.
- Define resource requests and limits.
- Understand the difference between readiness and liveness.
- A container can be Running while the Pod remains Not Ready.
- Kubernetes events provide valuable troubleshooting evidence.
- Service endpoints help diagnose application connectivity problems.
- Always verify application functionality after remediation.

---

## Status

**Completed**

This project is part of my ongoing Cloud Engineering Home Lab portfolio.