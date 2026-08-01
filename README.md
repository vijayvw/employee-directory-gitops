# 🚀 Employee Directory GitOps Platform

<p align="center">

  <img src="screenshots/banner.png" alt="Employee Directory GitOps Platform Banner">

</p>

<p align="center">

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Docker Hub](https://img.shields.io/badge/DockerHub-2496ED?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=github-actions&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white)
![NGINX Ingress](https://img.shields.io/badge/NGINX-Ingress-009639?logo=nginx&logoColor=white)
![Argo CD](https://img.shields.io/badge/ArgoCD-EF7B4D?logo=argo&logoColor=white)
![GitOps](https://img.shields.io/badge/GitOps-326CE5?logo=git&logoColor=white)
![Docker Multi-Arch](https://img.shields.io/badge/Multi--Arch-AMD64%20%7C%20ARM64-2496ED?logo=docker&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

</p>

---

## 📖 Project Overview

Employee Directory GitOps Platform is a cloud-native application that demonstrates a complete **GitOps Continuous Deployment pipeline** using modern DevOps tools and Kubernetes best practices.

Unlike a traditional deployment where developers manually deploy containers, this project follows a GitOps workflow in which **Git becomes the single source of truth**.

Every code change pushed to GitHub automatically:

- Builds a multi-architecture Docker image
- Pushes the image to Docker Hub
- Updates the Kubernetes Deployment manifest
- Commits the updated manifest back to GitHub
- Argo CD detects the Git change
- Kubernetes performs a rolling update automatically

No manual deployment commands are required after the initial bootstrap.

---

## ✨ Features

- Flask Web Application
- Employee CRUD Operations
- MySQL Persistent Database
- Redis Cache Layer
- Docker Multi-Architecture Images (AMD64 & ARM64)
- GitHub Actions CI Pipeline
- Docker Hub Image Registry
- GitOps Continuous Deployment
- Argo CD Automatic Synchronization
- Kubernetes Deployments
- ConfigMaps
- Secrets
- Persistent Volume Claims
- Readiness & Liveness Probes
- Rolling Updates
- NGINX Ingress
- Modern Responsive Dashboard UI
---

# 🏗️ Architecture

```text
                                    Developer
                                        │
                                        │
                                  git push origin main
                                        │
                                        ▼
                            GitHub Repository (main)
                                        │
                                        ▼
                           GitHub Actions CI Pipeline
                                        │
            ┌───────────────────────────┴───────────────────────────┐
            │                                                       │
            ▼                                                       ▼

   Build Multi-Architecture Docker Image              Update Kubernetes Deployment
         (AMD64 + ARM64)                              Image Tag (GitOps Manifest)

            │                                                       │
            ▼                                                       ▼

         Docker Hub                                  Commit Updated Manifest
                                                          to GitHub Repository

                                        │
                                        ▼

                             Argo CD Watches Repository

                                        │
                                        ▼

                           Detects New Git Commit Automatically

                                        │
                                        ▼

                        Synchronizes Kubernetes Desired State

                                        │
                                        ▼

                        Kubernetes Rolling Deployment Begins

                                        │
                        ┌───────────────┴───────────────┐
                        ▼                               ▼

                 Old Pods Terminated             New Pods Created

                                        │
                                        ▼

                         Employee Directory Platform (V2)
```

---

# ⚙️ Technology Stack

| Category | Technologies |
|-----------|--------------|
| Language | Python 3.12 |
| Framework | Flask |
| Web Server | Gunicorn |
| Database | MySQL |
| Cache | Redis |
| Containerization | Docker |
| Container Registry | Docker Hub |
| CI | GitHub Actions |
| GitOps | Argo CD |
| Container Orchestration | Kubernetes |
| Ingress | NGINX Ingress |
| Infrastructure | Kubernetes Cluster |
| Version Control | Git & GitHub |

---

# 📂 Repository Structure

```text
employee-directory-gitops/

│
├── app/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── static/
│   │     └── style.css
│   └── templates/
│         ├── base.html
│         ├── index.html
│         └── add_employee.html
│
├── kubernetes/
│   │
│   ├── argocd/
│   │      └── application.yaml
│   │
│   ├── 00-namespace.yaml
│   ├── 01-secrets.yaml
│   ├── 02-configmap.yaml
│   ├── 03-mysql-pvc.yaml
│   ├── 04-mysql-deployment.yaml
│   ├── 05-mysql-service.yaml
│   ├── 06-redis-deployment.yaml
│   ├── 07-redis-service.yaml
│   ├── 08-app-deployment.yaml
│   ├── 09-app-service.yaml
│   └── 10-ingress.yaml
│
├── .github/
│    └── workflows/
│          └── ci-cd.yml
│
└── README.md
```

---

# 🚀 Infrastructure Requirements

This repository is **Application GitOps Repository** only.

A Kubernetes cluster must already exist before deploying this application.

The cluster should already contain:

- Kubernetes Cluster
- Argo CD
- NGINX Ingress Controller
- Storage Class
- Metrics Server *(Optional)*

---

## Recommended Cluster

This project was designed to run on the Kubernetes cluster created using my

**k8s-cluster-automation**

project.

That project automatically provisions:

- Kubernetes Cluster
- Argo CD
- NGINX Ingress
- Metrics Server
- Storage Class

making this application ready to deploy immediately.

---

# 📥 Clone Repository

```bash
git clone https://github.com/vijayvw/employee-directory-gitops.git

cd employee-directory-gitops
```

---

# 🔐 Configure GitHub Secrets

Before pushing code, configure the following GitHub Repository Secrets.

| Secret Name | Description |
|--------------|------------|
| DOCKER_USERNAME | Docker Hub Username |
| DOCKER_PASSWORD | Docker Hub Access Token |

GitHub Actions uses these secrets to authenticate with Docker Hub and push Docker images.

---
# 🚀 Deploy Application

This project follows a **GitOps deployment model** using **Argo CD**.

Once Argo CD is installed and configured on the Kubernetes cluster, deploying the application requires only a single command.

```bash
kubectl apply -f kubernetes/argocd/application.yaml
```

The `Application` resource instructs Argo CD to monitor this Git repository and continuously synchronize the Kubernetes cluster with the manifests stored under the `kubernetes/` directory.

Once applied, Argo CD automatically:

- Creates the `emp-directory` namespace
- Creates Kubernetes Secrets
- Creates ConfigMaps
- Creates Persistent Volume Claims
- Deploys MySQL
- Deploys Redis
- Deploys the Employee Directory application
- Creates Kubernetes Services
- Configures the NGINX Ingress
- Continuously monitors the Git repository for changes

No additional `kubectl apply` commands are required after the initial bootstrap.

---

# 📦 Verify Deployment

Check all Kubernetes resources.

```bash
kubectl get all -n emp-directory
```

Example output:

```text
NAME                                READY   STATUS
employee-app-xxxxx                  1/1     Running
employee-app-yyyyy                  1/1     Running
mysql-xxxxx                         1/1     Running
redis-xxxxx                         1/1     Running
```

Check the Deployment.

```bash
kubectl get deployment -n emp-directory
```

Check the Services.

```bash
kubectl get svc -n emp-directory
```

Check the Ingress.

```bash
kubectl get ingress -n emp-directory
```

---

# ⚙️ Continuous Integration (GitHub Actions)

Every push to the **main** branch automatically triggers the GitHub Actions workflow.

The workflow performs the following tasks:

1. Checkout the repository
2. Configure Docker Buildx
3. Authenticate with Docker Hub
4. Build Multi-Architecture Docker Image
5. Push Docker Image to Docker Hub
6. Update Kubernetes Deployment image tag
7. Commit the updated manifest
8. Push changes back to GitHub

The Docker image is published with two tags:

```
latest
```

and

```
<Git Commit SHA>
```

This ensures every deployment references an immutable image version.

---

# 🐳 Docker Image

Images are automatically published to Docker Hub.

Example:

```
vijayvw/employee-app:latest

vijayvw/employee-app:a363295c9fc127d63b637a8ff19427ae1f00da6c
```

Supported Architectures:

- linux/amd64
- linux/arm64

This allows the application to run on both Intel/AMD servers and ARM-based systems such as AWS Graviton and Apple Silicon.

---

# 🔄 GitOps Continuous Deployment Workflow

The Kubernetes cluster is never updated manually.

Instead, Git becomes the **Single Source of Truth**.

Whenever a developer pushes code:

```
Developer
     │
     ▼
git push
     │
     ▼
GitHub Repository
     │
     ▼
GitHub Actions
     │
     ▼
Build Docker Image
     │
     ▼
Push Image to Docker Hub
     │
     ▼
Update Deployment Manifest
     │
     ▼
Commit Updated Manifest
     │
     ▼
Git Repository
     │
     ▼
Argo CD detects Git change
     │
     ▼
Synchronizes Kubernetes
     │
     ▼
Rolling Update
     │
     ▼
New Version Running
```

No administrator logs into the Kubernetes cluster to deploy a new version.

Everything is driven automatically from Git.

---

# ☸️ Kubernetes Resources

This project deploys the following Kubernetes resources.

| Resource | Purpose |
|----------|---------|
| Namespace | Isolates application resources |
| Secret | Stores MySQL credentials |
| ConfigMap | Application configuration |
| PersistentVolumeClaim | MySQL persistent storage |
| MySQL Deployment | Database |
| MySQL Service | Internal database access |
| Redis Deployment | Cache server |
| Redis Service | Internal Redis access |
| Employee Deployment | Flask application |
| Employee Service | Exposes the application |
| NGINX Ingress | External HTTP routing |

---

# ❤️ Health Checks

The application exposes two health endpoints.

### Liveness Probe

```
/health
```

Used by Kubernetes to determine whether the application process is still running.

---

### Readiness Probe

```
/ready
```

Checks connectivity to:

- MySQL
- Redis

Traffic is routed to the application only after all dependencies are available.

---

# 🚀 Rolling Updates

Application updates are performed using Kubernetes Rolling Updates.

Benefits include:

- Zero-downtime deployments
- Gradual pod replacement
- Automatic rollback capability
- High availability during upgrades

Every Git commit results in a new Deployment rollout managed by Kubernetes.
---

# 🔙 Rollback Strategy

This project follows **GitOps principles**, where the **Git repository is the single source of truth**.

Unlike traditional Kubernetes deployments, changes should **not** be rolled back manually using:

```bash
kubectl rollout undo deployment/employee-app -n emp-directory
```

Since Argo CD continuously watches the Git repository with automated synchronization enabled, any manual changes made directly in the Kubernetes cluster will be reconciled back to the desired state stored in Git.

## Recommended Rollback Process

Rollback is performed by reverting the Git commit.

```bash
git log --oneline

git revert <commit-id>

git push origin main
```

Once the commit is pushed:

1. GitHub Actions detects the new commit.
2. A new Docker image is built and pushed to Docker Hub.
3. The Kubernetes Deployment manifest is updated.
4. Argo CD detects the Git change.
5. Kubernetes performs a Rolling Update to the previous version.

This approach keeps Git, Argo CD, and the Kubernetes cluster synchronized.

---

# 📊 Application Dashboard

The application dashboard provides real-time deployment information including:

- Total Employees
- Redis Page View Counter
- Redis Cache Status
- Running Kubernetes Pod
- Application Version
- Namespace
- Deployment Platform
- GitOps Deployment Information

This makes the project useful for demonstrating Kubernetes concepts while providing a modern and responsive user interface.

---

# 📸 Project Walkthrough

The following screenshots demonstrate the complete GitOps workflow—from provisioning a Kubernetes cluster to automatically deploying new application versions using GitHub Actions, Docker Hub, Argo CD, and Kubernetes.

---

## 1️⃣ Kubernetes Cluster Ready

Three-node Kubernetes cluster with all required platform components installed.

- Kubernetes Control Plane
- Worker Nodes
- Argo CD
- NGINX Ingress
- Prometheus
- Grafana
- Local Path Storage

<p align="center">
<img src="screenshots/01-cluster-ready.png" width="100%">
</p>

---

## 2️⃣ Deploy the Application with a Single Command

The entire application is bootstrapped using only one command.

```bash
kubectl apply -f kubernetes/argocd/application.yaml
```

Argo CD immediately begins synchronizing all Kubernetes manifests stored in Git.

<p align="center">
<img src="screenshots/02-deploy.png" width="100%">
</p>

---

## 3️⃣ Employee Directory (Version 1)

Initial deployment of the Employee Directory application.

Features demonstrated:

- Flask Application
- MySQL Database
- Redis Page Counter
- Running Kubernetes Pod
- Employee Dashboard

<p align="center">
<img src="screenshots/03-dashboard-v1.png" width="100%">
</p>

---

## 4️⃣ Argo CD GitOps Dashboard

Argo CD continuously monitors the Git repository and ensures the Kubernetes cluster always matches the desired state.

Application Status:

- Healthy
- Synced
- Auto Sync Enabled

<p align="center">
<img src="screenshots/04-argocd.png" width="100%">
</p>

---

## 5️⃣ Employee CRUD Operations

Adding an employee stores the record inside MySQL while automatically invalidating the Redis cache.

<p align="center">
<img src="screenshots/05-add-employee.png" width="100%">
</p>

---

## 6️⃣ Redis Cache Demonstration

Subsequent requests are served directly from Redis, reducing database load and improving response time.

<p align="center">
<img src="screenshots/06-redis-cache.png" width="100%">
</p>

---

## 7️⃣ GitHub Actions Continuous Integration

Every push to the **main** branch automatically triggers the CI pipeline.

The workflow performs:

- Checkout Repository
- Docker Buildx
- Multi-Architecture Build
- Push Docker Image
- Update Kubernetes Manifest
- Commit Updated Image Tag
- Push Back to GitHub

<p align="center">
<img src="screenshots/07-github-actions.png" width="100%">
</p>

---

## 8️⃣ Employee Directory (Version 2)

After pushing updated source code, GitHub Actions automatically builds a new Docker image.

Argo CD detects the updated Kubernetes manifest and deploys the latest version automatically.

<p align="center">
<img src="screenshots/08-dashboard-v2.png" width="100%">
</p>

---

## 9️⃣ GitOps Automatic Synchronization

Argo CD detects the new Git commit and performs an automatic rolling update across the Kubernetes cluster.

Multiple ReplicaSets demonstrate deployment history while ensuring zero downtime.

<p align="center">
<img src="screenshots/09-argocd-rollout.png" width="100%">
</p>

---

## 🔟 Kubernetes Rolling Deployment

Kubernetes gradually replaces old Pods with newly created Pods running the latest Docker image.

This ensures:

- Zero Downtime
- High Availability
- Rolling Updates
- Automatic Deployment

<p align="center">
<img src="screenshots/10-scale.png" width="100%">
</p>

---

## 1️⃣1️⃣ Grafana Monitoring Dashboard

Prometheus continuously collects metrics while Grafana visualizes Kubernetes resource utilization in real time.

Monitoring includes:

- CPU Usage
- Memory Usage
- Pod Utilization
- Namespace Metrics
- Resource Requests & Limits

<p align="center">
<img src="screenshots/11-grafana.png" width="100%">
</p>

---

# 🚀 End-to-End GitOps Workflow

```text
Developer
    │
    │
    ▼
git push origin main
    │
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ├── Build Multi-Architecture Docker Image
    ├── Push Image to Docker Hub
    ├── Update Kubernetes Deployment Manifest
    └── Commit Updated Manifest
            │
            ▼
GitHub Repository
            │
            ▼
Argo CD
            │
            ▼
Detect Git Changes
            │
            ▼
Synchronize Cluster
            │
            ▼
Kubernetes Rolling Update
            │
            ▼
Employee Directory Platform Updated Automatically
```

This project demonstrates a complete production-style GitOps workflow where Git remains the **Single Source of Truth**.

No manual Docker builds.

No manual image updates.

No manual `kubectl apply`.

No manual Kubernetes deployments.

Every application update is fully automated through GitHub Actions, Docker Hub, Argo CD, and Kubernetes.

---

# 🛠 Troubleshooting

## Pods stuck in Init state

Check pod events.

```bash
kubectl describe pod <pod-name> -n emp-directory
```

---

## View application logs

```bash
kubectl logs -f deployment/employee-app -n emp-directory
```

---

## Check MySQL

```bash
kubectl get pods -n emp-directory

kubectl logs deployment/mysql -n emp-directory
```

---

## Check Redis

```bash
kubectl logs deployment/redis -n emp-directory
```

---

## Check Argo CD

```bash
kubectl get applications -n argocd
```

Application should display:

```
Healthy

Synced
```

---

## Check GitHub Actions

Navigate to

```
GitHub Repository

↓

Actions
```

Verify that the workflow completed successfully.

---

## Verify Docker Image

```bash
docker pull vijayvw/employee-app:latest
```

or

```bash
docker pull vijayvw/employee-app:<commit-sha>
```

---

# 🚀 Future Improvements

Planned enhancements include:

- Horizontal Pod Autoscaler (HPA)
- Prometheus Monitoring
- Grafana Dashboards
- Helm Chart Support
- Argo Rollouts (Blue/Green Deployments)
- Canary Deployments
- Argo Image Updater
- External Secrets Operator
- cert-manager with HTTPS
- Multi-Environment GitOps (Development, Staging, Production)
- PostgreSQL Support
- JWT Authentication
- Role-Based Access Control (RBAC)
- Kubernetes Network Policies

---

# 📚 Related Projects

### Kubernetes Cluster Automation

Provision a production-ready Kubernetes cluster using Terraform and Ansible with:

- Kubernetes
- Argo CD
- NGINX Ingress
- Metrics Server
- Storage Class

---

### GitOps WordPress Platform

A complete GitOps implementation for WordPress using:

- Docker
- Kubernetes
- Argo CD
- GitHub Actions

---

### AWS Event Driven File Upload

A serverless event-driven architecture using:

- Amazon S3
- Lambda
- SNS
- SQS
- CloudWatch

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

If you discover a bug or have an idea for an enhancement, please open an Issue or submit a Pull Request.

---

# 📄 License

This project is released under the MIT License.

---

# 👨‍💻 Author

## Vijay VW

Cloud Engineer • DevOps Engineer • Kubernetes Enthusiast

### Connect with me

## Vijay vw

- 🌐 **Portfolio:** [vijayvw.in](https://vijayvw.in)
- 💼 **LinkedIn:** [Vijay VW](https://www.linkedin.com/in/vijay-vw-417623197/)
- 💻 **GitHub:** [@vijayvw](https://github.com/vijayvw)

---

## ⭐ Support the Project

If you found this project useful, please consider giving it a ⭐ on GitHub.

It helps others discover the project and motivates further improvements.

---

# 🙏 Acknowledgements

Special thanks to the open-source community and the maintainers of:

- Flask
- Docker
- Kubernetes
- Redis
- MySQL
- GitHub Actions
- Argo CD
- NGINX Ingress

for building the incredible tools that made this project possible.