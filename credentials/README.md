# Credentials

**SENSITIVE: Do not share or expose these credentials**

## Proxmox

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| pve02 Web UI | https://10.88.140.164:8006 | root | (your root password) |

## Wazuh (Security Monitoring)

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| Wazuh Dashboard | https://10.88.140.202:443 | admin | *B96Y7a0t8Ep9cw+z0RSevdRHwLnsiay |
| Wazuh VM SSH | 10.88.140.202 | wazuh | WazuhServer2024! |

## Kubernetes (k3s)

### Monitoring Stack

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| Grafana | http://10.43.246.106 (cluster IP) | admin | cortex-admin |
| Prometheus | http://10.43.55.247:9090 (cluster IP) | - | - |
| Alertmanager | http://10.43.232.183:9093 (cluster IP) | - | - |
| Longhorn UI | http://10.43.166.3 (cluster IP) | - | - |

### k3s Access

```bash
# Copy kubeconfig from master
ssh root@10.88.140.164 'pct exec 300 -- cat /etc/rancher/k3s/k3s.yaml'

# Replace 127.0.0.1 with 10.88.145.170 in the kubeconfig
```

### k3s Node Token
```
K10b80418a0fa4f6be0a1162f527d14df167545374ac04392dc950cd4d574f4c3bd::server:68e3cc958673fc76ef61cb1be3df8d3e
```

## API Keys

| Service | Key |
|---------|-----|
| Anthropic API | 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 |

## GitHub

| Repo | URL | Visibility |
|------|-----|------------|
| cortex | https://github.com/ry-ops/cortex | Private |
| cortex-docker | https://github.com/ry-ops/cortex-docker | Private |
| k3s-gitops | https://github.com/ryandahlberg/playbooks | Private |
| infrastructure-docs | https://github.com/ry-ops/infrastructure-docs | Private |
