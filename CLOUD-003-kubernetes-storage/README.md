# CLOUD-003 — Kubernetes Persistent Storage

## Overview

This project demonstrates how Kubernetes PersistentVolumes and PersistentVolumeClaims can be used to preserve application data independently of the Pod lifecycle.

The lab uses an NGINX application running in Kubernetes with a PersistentVolumeClaim mounted to the NGINX web directory. Data is written to the mounted volume, the running Pod is intentionally deleted, and the replacement Pod verifies that the original data is still available.

The project also includes a troubleshooting scenario where a Deployment references a non-existent PersistentVolumeClaim, causing a Pod to remain in a Pending state.

---

## Technologies

- Kubernetes
- Docker Desktop
- NGINX
- YAML
- Git
- GitHub
- PowerShell

---

## Architecture

```text
NGINX Deployment
        |
        v
       Pod
        |
        v
/usr/share/nginx/html
        |
        v
PersistentVolumeClaim
    app-storage
        |
        v
PersistentVolume
        |
        v
Persistent Data