# 🚀 Deploy Prometheus and Grafana on Kubernetes using Terraform & Helm

## 📘 Project Overview

This project demonstrates how to provision a Kubernetes cluster and deploy a monitoring stack (Prometheus and Grafana) using **Infrastructure as Code (IaC)** tools — Terraform and Helm. It emphasizes automation, reproducibility, and real-time visualization of metrics in a Kubernetes environment.

---

## 🎯 Objectives

- Provision a Kubernetes cluster (Minikube/local or cloud)
- Install and configure Helm
- Deploy Prometheus & Grafana using Helm charts
- Connect Grafana with Prometheus
- Automate entire stack deployment using Terraform

---

## ⚙️ Technology Stack

| Component       | Description                          |
|----------------|--------------------------------------|
| Ubuntu          | Host OS for setup                    |
| Docker          | Container engine                     |
| Minikube        | Local Kubernetes cluster             |
| Terraform       | Infrastructure as Code               |
| Helm            | Kubernetes package manager           |
| Prometheus      | Monitoring tool                      |
| Grafana         | Metrics visualization tool           |

---

## 🧰 Prerequisites

Ensure the following tools are installed:

- Docker
- Minikube
- kubectl
- Terraform
- Helm

Install them using:

sudo apt update && sudo apt install -y docker.io curl unzip
🛠️ Setup Instructions
1. Start Kubernetes Cluster (Minikube)

minikube start --driver=docker
2. Install Helm & Add Repositories

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
🔨 Deploy Monitoring Stack Using Terraform
1. Clone This Repo

git clone https://github.com/yourusername/prometheus-grafana-terraform.git
cd prometheus-grafana-terraform
2. Terraform Files
main.tf defines Helm releases for Prometheus and Grafana.

variables.tf (optional) for custom values.

outputs.tf (optional) to show access info.

3. Initialize and Apply Terraform

terraform init
terraform apply -auto-approve
📊 Access the Monitoring Stack
Prometheus

kubectl port-forward -n monitoring svc/prometheus-server 9090
# Access: http://localhost:9090
Grafana

kubectl port-forward -n monitoring svc/grafana 3000:80

# Get admin password
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode
# Access: http://localhost:3000 (login as admin)
🧭 Architecture Diagram

Terraform → Kubernetes Cluster (via Minikube)
        └──> Helm Deploys:
              ├── Prometheus (port 9090)
              └── Grafana (port 3000)

Grafana Dashboard (http://localhost:3000)

Terminal output of running pods

📝 Conclusion
Using Terraform and Helm to automate the deployment of Prometheus and Grafana provides a powerful way to monitor Kubernetes clusters. This setup ensures consistency, scalability, and full observability into your microservices and infrastructure.
