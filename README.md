# Monitoring Stack - GitOps

Flux CD GitOps repository for Kubernetes monitoring infrastructure.

## Components

| Component | Version | Description |
|-----------|---------|-------------|
| Kube-Prometheus-Stack | 72.x | Prometheus, Alertmanager, Node Exporter, Kube-State-Metrics |
| Grafana Operator | 5.x | Manages Grafana instances via CRDs |
| Grafana | 11.4.0 | Visualization and dashboards |

## Structure

```
├── clusters/my-cluster/
│   ├── infrastructure.yaml
│   └── monitoring-stack.yaml
└── infrastructure/
    ├── base/          # HelmRepositories
    ├── controllers/   # HelmReleases
    └── configs/       # Grafana CRDs
```

## CI/CD

| Workflow | Trigger | Description |
|----------|---------|-------------|
| CI/CD | Push/PR | YAML lint, Kubernetes validation, Flux check |
| Release | Push to main | Auto version bump and release |

## Deployment

```bash
flux get kustomizations --watch
kubectl get pods -n monitoring
kubectl port-forward svc/grafana-service -n monitoring 3000:3000
```