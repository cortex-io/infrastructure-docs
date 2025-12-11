# Services

## Wazuh (Security Monitoring)

| Property | Value |
|----------|-------|
| Type | VM (VMID 201) |
| IP | 10.88.140.202 |
| Version | v4.14.1 |
| Components | Manager, Indexer, Dashboard (all-in-one) |

### Access

| Interface | URL | Credentials |
|-----------|-----|-------------|
| Dashboard | https://10.88.140.202:443 | admin / *B96Y7a0t8Ep9cw+z0RSevdRHwLnsiay |
| SSH | ssh wazuh@10.88.140.202 | wazuh / WazuhServer2024! |

### Monitored Agents

| ID | Name | IP | OS | Status |
|----|------|-----|-----|--------|
| 000 | wazuh-server | 127.0.0.1 | Ubuntu 24.04 | Active |
| 001 | k3s-worker-1 | 10.88.145.171 | Debian 13 | Active |
| 002 | k3s-worker-2 | 10.88.145.172 | Debian 13 | Active |
| 003 | k3s-master | 10.88.145.170 | Debian 13 | Active |

### Management Commands

```bash
# SSH to Wazuh server
ssh wazuh@10.88.140.202

# List agents
sudo /var/ossec/bin/agent_control -l

# Agent status
sudo systemctl status wazuh-manager

# View logs
sudo tail -f /var/ossec/logs/ossec.log
```

---

## Grafana (Monitoring Dashboard)

| Property | Value |
|----------|-------|
| Type | k8s Pod |
| Namespace | monitoring |
| Chart | kube-prometheus-stack |

### Access

```bash
# Port forward to access locally
kubectl port-forward -n monitoring svc/kube-prometheus-stack-grafana 3000:80

# Then browse to http://localhost:3000
# Login: admin / cortex-admin
```

---

## Prometheus (Metrics)

| Property | Value |
|----------|-------|
| Type | k8s Pod |
| Namespace | monitoring |
| Retention | 15 days |
| Storage | 50GB (Longhorn PVC) |

### Access

```bash
kubectl port-forward -n monitoring svc/kube-prometheus-stack-prometheus 9090:9090
# Browse to http://localhost:9090
```

---

## Longhorn (Storage)

| Property | Value |
|----------|-------|
| Type | k8s DaemonSet |
| Namespace | longhorn-system |
| Replicas | 3 |

### Access

```bash
kubectl port-forward -n longhorn-system svc/longhorn-frontend 8080:80
# Browse to http://localhost:8080
```

---

## Cortex (AI Orchestration)

| Property | Value |
|----------|-------|
| Type | k8s Deployment |
| Namespace | cortex |
| Architecture | Mixture of Experts (MoE) |

### Master Agents

| Name | Purpose |
|------|---------|
| coordinator-master | Task routing and orchestration |
| development-master | Feature implementation, bug fixes |
| security-master | Security audits, vulnerability scanning |
| inventory-master | Repository cataloging |
| cicd-master | CI/CD pipeline management |

---

## Netdata (Real-time Monitoring)

| Property | Value |
|----------|-------|
| Type | k8s DaemonSet |
| Namespace | default |
| Nodes | All k3s nodes |
