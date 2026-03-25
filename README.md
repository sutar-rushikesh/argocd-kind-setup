# 🚀 ArgoCD Setup on Kind (Kubernetes)

## 📌 Overview
This project demonstrates how to set up **ArgoCD on a Kubernetes cluster using Kind**.

---

## 🏗️ Architecture
GitHub Repo → ArgoCD → Kubernetes (Kind Cluster)

---

## ⚙️ Prerequisites
- Docker
- Kind
- kubectl
- Helm
- EC2 / Linux machine

---

## 🚀 Setup Steps

### 1. Create Kind Cluster
![Cluster Created](screenshots/step_1.png)

### 2. Verify Cluster
![Cluster Info](screenshots/step_2.png)

### 3. Install ArgoCD
![Helm Install](screenshots/step_3.png)

### 4. Verify Pods & Services
![Pods](screenshots/step_4.png)

### 5. Open Security Group Port
![Security Group](screenshots/step_5.png)

### 6. Access ArgoCD UI
![ArgoCD UI](screenshots/step_6.png)

---

## 🧪 Testing
```bash
kubectl get pods -n argocd
```

---

## 🧨 Destroy
```bash
kind delete cluster --name argocd-cluster
```

---

## 💡 Key Learnings
- GitOps using ArgoCD
- Kubernetes cluster setup via Kind
- Helm-based installation
