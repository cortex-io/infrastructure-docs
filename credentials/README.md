# Credentials

**SENSITIVE: Do not share or expose these credentials**

## Proxmox

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| pve01 Web UI | https://10.88.140.164:8006 | root | (your root password) |

## Wazuh (Security Monitoring)

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| Wazuh Dashboard | https://10.88.140.202:443 | admin | *B96Y7a0t8Ep9cw+z0RSevdRHwLnsiay |
| Wazuh VM SSH | 10.88.140.202 | wazuh | WazuhServer2024! |

## Kubernetes (k3s)

### Monitoring Stack (via Traefik Ingress + Port Forward)

Add these entries to `/etc/hosts` pointing to pve01 (port forward):
```
10.88.140.164 grafana.cortex.local prometheus.cortex.local alertmanager.cortex.local longhorn.cortex.local traefik.cortex.local
```

A socat port forward runs on pve01:8080 -> k3s-master:31080 (Traefik NodePort).

| Service | URL | Username | Password |
|---------|-----|----------|----------|
| Grafana | http://grafana.cortex.local:8080 | admin | cortex-admin |
| Prometheus | http://prometheus.cortex.local:8080 | - | - |
| Alertmanager | http://alertmanager.cortex.local:8080 | - | - |
| Longhorn UI | http://longhorn.cortex.local:8080 | - | - |
| Traefik Dashboard | http://traefik.cortex.local:8080/dashboard/ | - | - |

**Alternative: Port Forward Access**
```bash
kubectl port-forward -n monitoring svc/kube-prometheus-stack-grafana 3000:80
# Browse to http://localhost:3000
```

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
