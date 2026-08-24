# ☁️ Cloud Engineering Home Lab

Welcome to my Cloud Engineering Home Lab.

I created this repository to document my hands-on journey with cloud infrastructure, Kubernetes, DevOps, automation, Infrastructure as Code, and troubleshooting.

My goal is to go beyond studying concepts and build practical experience by completing labs that simulate tasks and incidents a Cloud, DevOps, or Platform Engineer may encounter in a real environment.

Each project includes the configuration files used to build the environment along with documentation explaining what I implemented, tested, troubleshot, and learned.

---

## 🛠️ Technologies

This repository will include hands-on work with:

* ☸️ Kubernetes
* ☁️ Amazon Web Services (AWS)
* 🏗️ Terraform
* 📦 Helm
* 🌱 Git & GitHub
* ⚙️ Ansible
* 🔄 CI/CD
* 🐧 Linux
* 📊 Monitoring & Observability
* 🔐 Cloud & Container Security
* 🐳 Containers

---

# 🧪 Labs

## CLOUD-001 — Kubernetes NGINX Deployment

My first lab focused on deploying and managing an NGINX application inside Kubernetes.

### Skills Practiced

* Creating Kubernetes YAML manifests
* Deployments
* Pods
* ReplicaSets
* Services
* Labels and selectors
* ClusterIP networking
* Port forwarding
* Container logs
* Kubernetes events
* Horizontal scaling
* Desired-state management
* Kubernetes self-healing
* Rolling updates
* Deployment rollbacks
* Application health verification
* Git version control

### Architecture

```text
                    User Browser
                         |
                  localhost:8080
                         |
                kubectl port-forward
                         |
                  nginx-service
                    ClusterIP
                         |
              +----------+----------+
              |          |          |
           NGINX      NGINX      NGINX
            Pod        Pod        Pod
```

The application was initially deployed with one replica and later scaled to three replicas.

I also intentionally deleted a running Pod to verify Kubernetes self-healing. The Deployment controller detected that the actual state no longer matched the desired state and automatically created a replacement Pod.

A rolling update was then performed to change the NGINX container version, followed by a rollback to practice recovering from a problematic application release.

---

## CLOUD-002 — Kubernetes Troubleshooting

This lab focuses on diagnosing and resolving common Kubernetes workload failures.

Instead of only working with healthy deployments, I intentionally introduce configuration problems and troubleshoot them using Kubernetes tooling.

### Troubleshooting Workflow

```text
Issue Reported
      |
      v
Check Pod Status
      |
      v
Describe Workload
      |
      v
Review Events
      |
      v
Inspect Logs
      |
      v
Identify Root Cause
      |
      v
Apply Fix
      |
      v
Verify Recovery
```

### Scenarios

* `ImagePullBackOff`
* `ErrImagePull`
* `CrashLoopBackOff`
* Incorrect container images
* Service selector failures
* Container port issues
* Application connectivity problems

Additional troubleshooting scenarios will be added as the lab progresses.

---

# 🔍 Kubernetes Troubleshooting Commands

Some of the commands I'm practicing throughout these labs include:

```bash
kubectl get pods
kubectl get pods -o wide
kubectl get deployments
kubectl get services
kubectl describe pod <pod-name>
kubectl describe deployment <deployment-name>
kubectl logs <pod-name>
kubectl logs -f <pod-name>
kubectl get events
kubectl get events -A
kubectl rollout status deployment/<deployment-name>
kubectl rollout history deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name>
```

The goal is not simply to memorize commands, but to understand when and why each command is useful during deployment validation and troubleshooting.

---

# 🚧 Upcoming Labs

I plan to continue expanding this repository with projects covering:

### Kubernetes

* ConfigMaps and Secrets
* Persistent Volumes
* Persistent Volume Claims
* Resource requests and limits
* Liveness and readiness probes
* Namespaces
* RBAC
* Ingress
* Helm deployments
* Advanced troubleshooting

### Terraform

* AWS EC2 provisioning
* VPC creation
* Public and private subnets
* Route tables
* Security groups
* Internet gateways
* Terraform variables
* Outputs
* Modules
* Remote state
* Infrastructure lifecycle management

### AWS

* IAM
* EC2
* VPC
* S3
* CloudWatch
* Load Balancers
* Auto Scaling
* Route 53
* EKS

### DevOps

* Git branching workflows
* CI/CD pipelines
* Helm
* Ansible
* Infrastructure as Code
* GitOps
* Argo CD
* Prometheus
* Grafana
* Container security scanning

---

# 🎯 Long-Term Project Goal

The long-term goal is to combine these technologies into a complete cloud-native environment.

```text
                    GitHub
                       |
                       v
                  CI/CD Pipeline
                       |
                       v
                   Terraform
                       |
                       v
                       AWS
                       |
              +--------+--------+
              |                 |
             VPC               IAM
              |
             EKS
              |
          Kubernetes
              |
        +-----+-----+
        |           |
       Helm       Argo CD
        |
    Applications
        |
   +----+----+
   |         |
Prometheus  Grafana
```

This will allow me to practice the full lifecycle of cloud infrastructure:

**Build → Deploy → Automate → Monitor → Troubleshoot → Secure → Improve**

---

# 📚 Documentation

In addition to maintaining the code in this repository, I am documenting the labs with screenshots and technical walkthroughs.

The documentation focuses on:

* What I built
* Why I configured it that way
* Commands used
* Problems encountered
* Troubleshooting methodology
* Root-cause analysis
* Solutions implemented
* Lessons learned

This allows me to reinforce the technical concepts while maintaining a record of my hands-on progress.

---

# ⚠️ Security

This repository is intended for educational and portfolio purposes.

Sensitive information such as the following should never be committed:

* AWS access keys
* API tokens
* Passwords
* Private keys
* `.env` files
* Terraform state containing sensitive data
* Kubernetes Secrets
* kubeconfig credentials

Repository exclusions are managed through `.gitignore` where appropriate.

---

# 📈 Progress

This repository is actively being expanded as I work through additional Cloud Engineering, Kubernetes, AWS, Terraform, and DevOps labs.

The goal is continuous hands-on development and progressively more realistic infrastructure projects.
