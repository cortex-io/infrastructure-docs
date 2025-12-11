# k3s Kubernetes Cluster

## Cluster Overview

| Property | Value |
|----------|-------|
| Distribution | k3s |
| Version | Latest stable |
| Nodes | 3 (1 server, 2 agents) |
| CNI | Flannel (default) |
| Storage | Longhorn |
| GitOps | Flux CD |

## Nodes

| Role | Hostname | IP | CTID |
|------|----------|-----|------|
| Server | k3s-master | 10.88.145.170 | 300 |
| Agent | k3s-worker-1 | 10.88.145.171 | 301 |
| Agent | k3s-worker-2 | 10.88.145.172 | 302 |

## Namespaces

| Namespace | Purpose |
|-----------|---------|
| flux-system | Flux CD GitOps controllers |
| cert-manager | TLS certificate management |
| longhorn-system | Longhorn distributed storage |
| monitoring | Prometheus, Grafana, Alertmanager |
| keda | Kubernetes Event-driven Autoscaling |
| cortex | Cortex AI orchestration system |

## Installed Components

### Core Infrastructure
- **Flux CD** - GitOps continuous deployment
- **Cert-Manager** - TLS certificate automation
- **Longhorn** - Distributed block storage
- **KEDA** - Event-driven autoscaling

### Monitoring
- **Prometheus** - Metrics collection
- **Grafana** - Dashboards and visualization
- **Alertmanager** - Alert routing
- **Netdata** - Real-time monitoring

### Applications
- **Cortex** - AI orchestration with MoE architecture
  - coordinator-master
  - development-master
  - security-master
  - inventory-master
  - cicd-master

## Access

### kubectl from local machine

```bash
# Get kubeconfig
ssh root@10.88.140.164 'pct exec 300 -- cat /etc/rancher/k3s/k3s.yaml' > ~/.kube/k3s-config

# Edit to replace 127.0.0.1 with 10.88.145.170
sed -i '' 's/127.0.0.1/10.88.145.170/g' ~/.kube/k3s-config

# Use the config
export KUBECONFIG=~/.kube/k3s-config
kubectl get nodes
```

### kubectl from k3s-master

```bash
ssh root@10.88.140.164 'pct exec 300 -- kubectl get nodes'
```

## Service Access

Services are on ClusterIPs. To access from outside:

```bash
# Port forward Grafana
kubectl port-forward -n monitoring svc/kube-prometheus-stack-grafana 3000:80

# Port forward Prometheus
kubectl port-forward -n monitoring svc/kube-prometheus-stack-prometheus 9090:9090

# Port forward Longhorn UI
kubectl port-forward -n longhorn-system svc/longhorn-frontend 8080:80
```

## GitOps Repository

The cluster is managed via Flux CD from:
- **Repo**: `/Users/ryandahlberg/Projects/playbooks/k3s-gitops`
- **Path**: `clusters/cortex-k3s/`

## Wazuh Agents

All k3s nodes have Wazuh agents installed for security monitoring:

| Node | Agent ID | Status |
|------|----------|--------|
| k3s-master | 003 | Active |
| k3s-worker-1 | 001 | Active |
| k3s-worker-2 | 002 | Active |
