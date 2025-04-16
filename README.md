# Kubernetes Monitoring with Prometheus Operator & Grafana

A hands-on project demonstrating how to deploy a full Kubernetes observability stack using **Minikube**, **Prometheus Operator**, **Grafana**, and **Helm** — all customized for a local development environment.

---

##  Project Overview
This project sets up a local Kubernetes cluster using Minikube and deploys the Prometheus monitoring stack via Helm. A custom Grafana dashboard was created to track critical metrics like:

-  Pod count per namespace
-  Node CPU and memory usage
- Pod restart counts
- Disk utilization per mount point

---

## Tools & Technologies
| Tool          | Purpose                                |
|---------------|-----------------------------------------|
| **Minikube**  | Local Kubernetes cluster                |
| **Docker**    | Container runtime for Minikube          |
| **Helm**      | Package manager to deploy K8s apps      |
| **Prometheus**| Metric collection and time-series store |
| **Grafana**   | Dashboard visualization layer            |
| **kubectl**   | Kubernetes CLI to manage cluster        |

---

## Step-by-Step Approach

### 1. **Set up Minikube on Windows**
- Driver: Docker
- Started via:
  ```bash
  minikube start --driver=docker
  ```

### 2. **Install Prometheus Stack via Helm**
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
kubectl create namespace monitoring
helm install kube-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring
```

### 3. **Access Services**
- **Prometheus UI**: `kubectl port-forward svc/kube-prometheus-kube-prome-prometheus -n monitoring 9090`
- **Grafana UI**: `kubectl port-forward svc/kube-prometheus-grafana -n monitoring 3000`

### 4. **Login to Grafana**
- Username: `admin`
- Password:
  ```bash
  kubectl get secret kube-prometheus-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 -d
  ```

---

##  Dashboard Panels Implemented
- **Pods by Namespace** — Track how workloads are distributed
- **Node CPU Usage** — Live gauge for node CPU utilization
- **Memory Usage per Node** — Percent used out of total
- **Disk Usage** — Calculated via PromQL from `node_exporter`
- **Pod Restarts** — Grouped by namespace + pod name

---

## Exported Dashboard
The entire dashboard is exported as JSON and included here:
```
/dashboard/k8s-monitoring-dashboard.json
```

To import in Grafana:
1. Go to Dashboards > Import
2. Upload the JSON file or paste its contents

---

##  Notes & Insights
- Used only open-source tools locally — no cloud dependencies.
- Adjusted PromQL queries to fit **Minikube’s mount points**.
- Tweaked thresholds and units for readability.
- Refined legend formatting and titles for polish.

---

## Folder Structure
```
kubernetes-Monitoring-with-Prometheus-Operator/
├── dashboard/
│   └── k8s-monitoring-dashboard.json
├── README.md
```

---

## Acknowledgments
- Prometheus Community Helm Charts
- Grafana Labs
- CNCF ecosystem

---

## Author
**Vamshi Mekala**  
GitHub: [Vamshikiran0301](https://github.com/Vamshikiran0301)

---

✅ Project Completed: April 2025
