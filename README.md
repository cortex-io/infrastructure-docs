# RyOps Infrastructure Documentation

Private documentation for homelab infrastructure.

**WARNING: This repository contains sensitive credentials. Never make this repository public.**

## Quick Links

- [Credentials](credentials/README.md) - All service passwords and API keys
- [Proxmox](proxmox/README.md) - Hypervisor nodes and VMs/LXCs
- [Kubernetes](kubernetes/k3s/README.md) - k3s cluster documentation
- [Services](services/README.md) - Running services (Wazuh, n8n, etc.)
- [Network](network/README.md) - Network topology and VLANs

## Infrastructure Overview

```
                    Internet
                        |
                   [OPNsense]
                        |
        ┌───────────────┼───────────────┐
        |               |               |
   VLAN 140        VLAN 145        VLAN 150
   (Default)       (k3s/Talos)     (Future)
        |               |
   ┌────┴────┐     ┌────┴────┐
   |         |     |         |
  pve02   Wazuh   k3s      Talos
          VM      Cluster   (planned)
```

## Proxmox Nodes

| Node | IP | Purpose |
|------|-----|---------|
| pve02 | 10.88.140.164 | Main hypervisor |

## Last Updated

2024-12-11
