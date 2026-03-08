# Monitoring & Observability

This document explains how monitoring and observability are implemented in the ML GitOps Automation Platform.

The project integrates **Prometheus and Grafana** to collect, store, and visualize application and system metrics.

The monitoring stack provides visibility into:

- API request rate
- Request latency
- CPU usage
- Memory usage
- Kubernetes cluster health

---

# Observability Architecture

The monitoring system consists of three main components.

| Component | Role |
|--------|------|
| Prometheus | Collects and stores metrics |
| Grafana | Visualizes metrics using dashboards |
| FastAPI Metrics Endpoint | Exposes application metrics |

Data flow: 
FastAPI App -> /metrics endpoint -> Prometheus -> Grafana Dashboards

---

# Prometheus Setup

Prometheus is installed in the Kubernetes cluster using **Helm** and the **kube-prometheus-stack** chart.

This stack installs:

- Prometheus server
- Alertmanager
- Node exporter
- Kubernetes monitoring components

Prometheus automatically scrapes metrics from configured targets.

---

# FastAPI Metrics Integration

The FastAPI application exposes metrics using the **Prometheus Python client library**.

Metrics are available through the endpoint:/metrics

Example metrics collected: 
```yaml
ml_app_requests_total
ml_app_request_latency_seconds
```
These metrics help track application
performance.
# Example Metrics
### Request Count
Counts the total number of API requests.
```yaml
ml_app_requests_total
```

---

### Request Latency

Measures how long each request takes.

```yaml 
ml_app_request_latency_seconds
```

---

# Prometheus Scraping

Prometheus collects application metrics using a **ServiceMonitor** resource.

The ServiceMonitor tells Prometheus:

- Which Kubernetes service to monitor
- Which endpoint exposes metrics
- How frequently metrics should be collected

Example ServiceMonitor configuration:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: ml-app-monitor
spec:
  selector:
    matchLabels:
      app: ml-app
  endpoints:
    - port: http
      path: /metrics
      interval: 15s
```
Prometheus then automatically discovers the application metrics

## Grafana Dashboards
Grafana is used to visualize metrics collected by
Prometheus.
Dashboards provide real-time insights into
system behavior.

The dashboards display:
-Request rate
- API latency
- CPU usage
- Memory usage
- Kubernetes node health

Grafana connects to Prometheus as its data
source.

## Monitoring Queries
Example Prometheus query used to track
request rate:
```yaml
rate(ml_app_requests_total[1m])
```
This shows the number of requests per second.
Other useful queries include:
Total Requests
```yaml
ml_app_requests_total
```

Request Latency
```yaml
ml_app_request_latency_seconds
```

## Benefits of Monitoring
The observability stack provides several
important advantages.

### Performance Monitoring
Track how the application behaves under load.

### Debugging Support
Identify slow requests or performance issues.

### System Visibility
Monitor Kubernetes nodes, pods, and resource
usage.

### Production Readiness
Observability is essential for running reliable
production systems.

## Monitoring Workflow
The monitoring system works as follows:

1. FastAPl application exposes metrics
2. Prometheus scrapes metrics from the /metrics endpoint
3. Prometheus stores time-series data
4. Grafana queries Prometheus
5. Dashboards visualize system performance

## Monitoring Summary
The monitoring system provides full visibility into
the application and infrastructure.

Key capabilities:
- Application metrics collection
- Kubernetes cluster monitoring
- Real-time performance dashboards
- Request rate and latency tracking
This setup ensures that the ML application can
be monitored effectively in a production-style
environment.