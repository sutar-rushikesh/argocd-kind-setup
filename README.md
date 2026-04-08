# 🚀 ArgoCD Setup on Kubernetes (Kind)

## 📌 Overview
Setup ArgoCD on Kind cluster using Helm with GitOps principles.

---

## 🧠 Theory
- Kind = Kubernetes in Docker
- ArgoCD = GitOps CD tool
- GitOps = Git is source of truth

---

## 🏗️ Architecture
GitHub → ArgoCD → Kubernetes (Kind)

---

## ⚙️ Prerequisites
- Docker
- kubectl
- Kind
- Helm

---

## 🚀 Steps

### Install Docker
Docker → Required for Kind to run containers as cluster nodes.
```bash
sudo apt-get update
sudo apt install docker.io -y
sudo usermod -aG docker $USER && newgrp docker
docker --version

docker ps
```

### Install Kind

Guide: https://kind.sigs.k8s.io/docs/user/quick-start/#installation 
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
```
### Install kubectl
Guide: https://kubernetes.io/docs/tasks/tools/ 
```bash
curl -LO https://dl.k8s.io/release/stable.txt/bin/linux/amd64/kubectl
```
### Install Helm
Guide: https://helm.sh/docs/intro/install/
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
```
### Create Cluster
Save your cluster config as kind-config.yaml:
```bash
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
networking:
  apiServerAddress: "172.31.19.178"   # Change this to your EC2 private IP (run "hostname -I" to check or from your EC2 dashboard)
  apiServerPort: 33893
nodes:
  - role: control-plane
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
```
Create Cluster
```bash
kind create cluster --name argocd-cluster
```
![Cluster](screenshots/step_1.png)

### Verify
```bash
kubectl get nodes
```
![Nodes](screenshots/step_2.png)

### Install ArgoCD
```bash
helm install argocd argo/argo-cd -n argocd
```
![Helm](screenshots/step_3.png)

### Verify Pods
```bash
kubectl get pods -n argocd
```
![Pods](screenshots/step_4.png)

### Open Port
![Security](screenshots/step_5.png)

### Access UI
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
![UI](screenshots/step_6.png)

---

## 🧪 Testing
```bash
kubectl get pods -n argocd
```
---

## 🧾 Common Commands
```bash
argocd login  
argocd app list  
argocd app sync  
```
---

## 🧨 Destroy
```bash
kind delete cluster --name argocd-cluster
```
