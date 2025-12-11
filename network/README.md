# Network Topology

## VLANs

| VLAN ID | Name | Subnet | Gateway | Purpose |
|---------|------|--------|---------|---------|
| 140 | Default | 10.88.140.0/24 | 10.88.140.1 | Default network, management |
| 145 | Kubernetes | 10.88.145.0/24 | 10.88.145.1 | k3s cluster, future Talos |
| 150 | Reserved | 10.88.150.0/24 | 10.88.150.1 | Future use |

## IP Allocations

### VLAN 140 (Default)

| IP | Hostname | Purpose |
|----|----------|---------|
| 10.88.140.1 | gateway | OPNsense router |
| 10.88.140.164 | pve02 | Proxmox hypervisor |
| 10.88.140.202 | wazuh-server | Wazuh SIEM (VM 201) |
| 10.88.140.252 | claude-vm | Claude agent VM |

### VLAN 145 (Kubernetes)

| IP | Hostname | Purpose |
|----|----------|---------|
| 10.88.145.1 | gateway | OPNsense router |
| 10.88.145.170 | k3s-master | k3s server (LXC 300) |
| 10.88.145.171 | k3s-worker-1 | k3s agent (LXC 301) |
| 10.88.145.172 | k3s-worker-2 | k3s agent (LXC 302) |
| 10.88.145.160-169 | reserved | Future Talos cluster |

## Kubernetes Networking

### Cluster Network
- **Pod CIDR**: 10.42.0.0/16 (k3s default)
- **Service CIDR**: 10.43.0.0/16 (k3s default)
- **CNI**: Flannel (VXLAN mode)

### Key ClusterIPs

| Service | IP | Port |
|---------|-----|------|
| kube-dns | 10.43.0.10 | 53 |
| Grafana | 10.43.246.106 | 80 |
| Prometheus | 10.43.55.247 | 9090 |
| Alertmanager | 10.43.232.183 | 9093 |
| Longhorn UI | 10.43.166.3 | 80 |

## Firewall Rules (OPNsense)

### Inter-VLAN
- VLAN 145 -> VLAN 140: Allow (k3s to Wazuh for agent communication)
- VLAN 140 -> VLAN 145: Allow (management access)

### Wazuh Ports
- TCP 1514: Agent communication
- TCP 1515: Agent enrollment
- TCP 443: Dashboard (HTTPS)
- TCP 9200: Indexer API

## DNS

- Primary: OPNsense (10.88.140.1)
- k8s internal: CoreDNS (10.43.0.10)

## Diagram

```
                        Internet
                            |
                      [OPNsense]
                       10.88.140.1
                       10.88.145.1
                            |
            ┌───────────────┼───────────────┐
            |               |               |
       VLAN 140        VLAN 145        VLAN 150
    10.88.140.0/24   10.88.145.0/24   10.88.150.0/24
            |               |               |
    ┌───────┴───────┐       |               |
    |               |       |           (reserved)
   pve02        wazuh    k3s cluster
 .164            .202       |
                     ┌──────┼──────┐
                     |      |      |
                  master  worker1 worker2
                   .170    .171    .172
```
