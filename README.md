# ArgoCD Monitoring Stack

This repository contains Kubernetes manifests for deploying a monitoring stack with ArgoCD, including:

- Prometheus (v3.2.1, Helm Chart 27.7.1)
- Prometheus Node Exporter (v1.9.0, Helm Chart 4.45.0)
- Grafana (v11.6.0, Helm Chart 8.11.0)

## Prerequisites

- Kubernetes cluster
- ArgoCD installed in your cluster
- `kubectl` configured to access your cluster

## Directory Structure

```
apps/
├── namespace.yaml
├── monitoring-app.yaml
├── prometheus/
│   └── application.yaml
├── node-exporter/
│   └── application.yaml
└── grafana/
    └── application.yaml
```

## Installation

1. Fork this repository and clone it to your local machine
2. Replace the placeholder repository URL in `apps/monitoring-app.yaml` with your own repository URL
3. Push the changes to your repository
4. Apply the parent application to your ArgoCD instance:

```bash
  kubectl apply -f apps/monitoring-app.yaml
```

ArgoCD will automatically create the monitoring namespace and deploy all the applications.

## Configuration

- The Prometheus server is configured with a 10Gi persistent volume
- Grafana is configured with a 5Gi persistent volume
- Grafana is pre-configured with a Prometheus data source

## Access

- Prometheus UI: Port-forward to the prometheus-server service
  ```
  kubectl port-forward svc/prometheus-server -n monitoring 9090:80
  ```

- Grafana UI: Port-forward to the grafana service
  ```
  kubectl port-forward svc/grafana -n monitoring 3000:80
  ```
  Default credentials: admin/admin (you will be prompted to change on first login) 