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
sudo apt-get update
sudo apt install docker.io -y

### Install Kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64

### Install kubectl
curl -LO https://dl.k8s.io/release/stable.txt/bin/linux/amd64/kubectl

### Install Helm
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4

### Create Cluster
kind create cluster --name argocd-cluster

![Cluster](screenshots/step_1.png)

### Verify
kubectl get nodes

![Nodes](screenshots/step_2.png)

### Install ArgoCD
helm install argocd argo/argo-cd -n argocd

![Helm](screenshots/step_3.png)

### Verify Pods
kubectl get pods -n argocd

![Pods](screenshots/step_4.png)

### Open Port
![Security](screenshots/step_5.png)

### Access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

![UI](screenshots/step_6.png)

---

## 🧪 Testing
kubectl get pods -n argocd

---

## 🧾 Common Commands
argocd login  
argocd app list  
argocd app sync  

---

## 🧨 Destroy
kind delete cluster --name argocd-cluster
