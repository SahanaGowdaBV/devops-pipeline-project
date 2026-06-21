# 🚀 DevOps Pipeline Project (Production-Grade)

## 📌 Overview

This project demonstrates a production-ready DevOps pipeline using:

* Docker (containerization)
* Kubernetes (deployment & orchestration)
* Helm (package management)
* GitHub Actions (CI/CD)

Supports:

* Standard Kubernetes deployment
* Helm-based production deployment
* Autoscaling (HPA)
* Zero-downtime rolling updates

---

# 🧰 Prerequisites (Install First)

## 🔹 Install Git

Download: https://git-scm.com/downloads

Verify:

```bash
git --version
```

---

## 🔹 Install Docker

Download: https://www.docker.com/products/docker-desktop/

Verify:

```bash
docker --version
```

---

## 🔹 Install Minikube

Download: https://minikube.sigs.k8s.io/docs/start/

Verify:

```bash
minikube version
```

---

## 🔹 Install kubectl

```bash
kubectl version --client
```

---

## 🔹 Install Helm

Download: https://helm.sh/docs/intro/install/

Verify:

```bash
helm version
```

---

# 📥 Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/devops-pipeline-project.git
cd devops-pipeline-project
```

---

# 🐳 Run Application Locally (Docker)

## Build Image

```bash
docker build -t devops-app .
```

## Run Container

```bash
docker run -p 3000:3000 devops-app
```

Test:

* http://localhost:3000
* http://localhost:3000/health

---

# ☸️ Kubernetes Deployment (Basic)

## Step 1: Start Minikube

```bash
minikube start
```

---

## Step 2: Load Docker Image into Minikube

```bash
minikube image load devops-app
```

---

## Step 3: Deploy to Kubernetes

```bash
kubectl apply -f k8s/
```

---

## Step 4: Verify

```bash
kubectl get pods
kubectl get svc
```

---

## Step 5: Access Application

```bash
minikube service devops-service
```

---

# 📦 Helm Deployment (Production Setup)

## Step 1: Enable Metrics Server (Required for Autoscaling)

```bash
minikube addons enable metrics-server
```

---

## Step 2: Install Helm Chart

```bash
helm install devops-release ./devops-chart
```

---

## Step 3: Verify Deployment

```bash
kubectl get pods
kubectl get svc
kubectl get hpa
```

---

## Step 4: Access Application

```bash
minikube service devops-service
```

---

# 🔄 Zero Downtime Deployment Test

Update image tag in:

```
devops-chart/values.yaml
```

Example:

```yaml
tag: "v2"
```

Then upgrade:

```bash
helm upgrade devops-release ./devops-chart
```

Check rollout:

```bash
kubectl rollout status deployment/devops-app
```

---

# 📈 Autoscaling Test (HPA)

## Generate Load

```bash
kubectl run -i --tty load-generator --image=busybox -- /bin/sh
```

Inside pod:

```bash
while true; do wget -q -O- http://devops-service; done
```

---

## Watch Scaling

```bash
kubectl get hpa -w
```

---

# 🧪 Health Checks

* Readiness Probe → ensures traffic only to healthy pods
* Liveness Probe → restarts unhealthy containers

Test:

```bash
curl http://localhost:3000/health
```

---

# 🧹 Cleanup

## Delete Kubernetes Resources

```bash
kubectl delete -f k8s/
```

---

## Delete Helm Release

```bash
helm uninstall devops-release
```

---

## Stop Minikube

```bash
minikube stop
```

---

# 📂 Project Structure

```
app/                  → Node.js app
k8s/                  → Kubernetes manifests
devops-chart/         → Helm chart
.github/workflows/    → CI/CD pipeline
Dockerfile            → Container config
```

---

# 🚀 Key Features

* Containerized microservice
* Kubernetes deployment (replicated pods)
* Helm-based production deployment
* Zero-downtime rolling updates
* Horizontal Pod Autoscaling (HPA)
* Health monitoring (liveness/readiness)

---

# 🔮 Future Improvements

* Add Ingress (NGINX)
* Add Prometheus + Grafana monitoring
* Add logging (EFK stack)
* Deploy to AWS EKS

---

# 🧠 Author

DevOps Engineer | Cloud | Kubernetes | CI/CD
