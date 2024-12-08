# LGTM Stack Deployment

## 1. Add Helm Repositories

Update Helm repositories for Grafana and Prometheus charts:

```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

## 2. Install Stack Components
Deploy each component of the monitoring stack using its specific Helm chart and configuration settings from the respective values.yaml file within each component's directory.

### Grafana

```
helm upgrade --install grafana grafana/grafana -f grafana/values.yaml -n monitoring 
```

### Promtail

```
helm upgrade --install promtail grafana/promtail -f promtail/values.yaml -n monitoring 
```

### Loki

```
helm upgrade --install loki grafana/loki -f loki/values.yaml -n monitoring 
```

### Tempo

```
helm upgrade --install tempo grafana/tempo -n monitoring
```

### Kube-Prometheus-Stack

```
helm upgrade --install kube-prometheus-stack prometheus-community/kube-prometheus-stack -f kube-prometheus-stack/values.yaml -n monitoring  --version 65.1.1
```

## 2. Add custom configmaps
Deploy custom Grafana dashboards
```
kubectl apply -f dashboards/custom-dashboards-configmap.yaml -n monitoring
```
