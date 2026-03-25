# 🚀 ArgoCD Setup on Kubernetes (Kind)

## 📌 Overview
This repository demonstrates how to set up **ArgoCD on a Kubernetes cluster (Kind)** using **Helm**.  
It follows DevOps best practices and provides a complete GitOps-ready environment.

---

## 🧠 What You Will Learn
- Kubernetes cluster setup using Kind
- Installing ArgoCD using Helm
- Accessing ArgoCD UI
- Understanding GitOps workflow
- Troubleshooting common issues

---

## 🏗️ Architecture

GitHub Repo --> ArgoCD --> Kubernetes (Kind Cluster)
                     |
                  UI / CLI

---

## ⚙️ Prerequisites

- Linux machine / EC2 instance
- Docker installed
- kubectl installed
- Kind installed
- Helm installed
- Open ports: 8080

---

## 🚀 Setup Steps

### 1️⃣ Install Docker
```bash
sudo apt-get update
sudo apt install docker.io -y
sudo usermod -aG docker $USER && newgrp docker
docker --version
```

---

### 2️⃣ Install Kind
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
kind version
```

---

### 3️⃣ Install kubectl
```bash
curl -LO "https://dl.k8s.io/release/stable.txt/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

---

### 4️⃣ Install Helm
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4
chmod 700 get_helm.sh
./get_helm.sh
```

---

### 5️⃣ Create Kind Cluster

Create a file `kind-config.yaml`:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
networking:
  apiServerAddress: "YOUR_PRIVATE_IP"
  apiServerPort: 33893
nodes:
  - role: control-plane
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
```

Create cluster:

```bash
kind create cluster --name argocd-cluster --config kind-config.yaml
```

Verify:

```bash
kubectl cluster-info
kubectl get nodes
```

---

### 6️⃣ Install ArgoCD using Helm

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update

kubectl create namespace argocd
helm install argocd argo/argo-cd -n argocd
```

Verify:

```bash
kubectl get pods -n argocd
kubectl get svc -n argocd
```

---

### 7️⃣ Access ArgoCD UI

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address=0.0.0.0
```

Open in browser:

https://<EC2_PUBLIC_IP>:8080

---

### 🔑 Get Admin Password

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d && echo
```

Login:
- Username: admin
- Password: (above output)

---

## 🧪 Testing

Check pods:

```bash
kubectl get pods -n argocd
```

Ensure all pods are in Running state.

---

## ❗ Common Issues & Fixes

### 🔴 Cluster not found
- Ensure correct API server IP in kind config

### 🔴 ArgoCD UI not accessible
- Check port-forward command
- Verify security group rules

### 🔴 Helm install failed
- Run `helm repo update`

---

## 🧨 Destroy Cluster

```bash
kind delete cluster --name argocd-cluster
```

---

## 💡 Key Takeaways

- ArgoCD enables GitOps-based deployments
- Helm provides flexibility for production setups
- Kind is ideal for local Kubernetes testing

---

## 📌 Author

**NavOps Academy**
DevOps | Kubernetes | GitOps
