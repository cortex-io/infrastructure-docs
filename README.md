<img src="docs/banner.svg" width="100%" alt="infrastructure-docs: the homelab underneath Cortex: Proxmox, K3s, networking and services. Part of the archived Cortex project.">

> [!NOTE]
> **Archived.** This repo is part of [Cortex](https://github.com/cortex-io), which is no longer under active development. It is kept as a working record: explore, fork and borrow freely, but no fixes or features are planned.

<p align="center"><sub><a href="https://github.com/cortex-io"><b>Cortex</b></a> &nbsp;·&nbsp; <a href="https://github.com/cortex-io/cortex">cortex</a> · <a href="https://github.com/cortex-io/cortex-platform">cortex-platform</a> · <a href="https://github.com/cortex-io/cortex-gitops">cortex-gitops</a> · <a href="https://github.com/cortex-io/cortex-k3s">cortex-k3s</a> · <a href="https://github.com/cortex-io/cortex-docs">cortex-docs</a> · <a href="https://github.com/cortex-io/cortex-construction-hq">cortex-construction-hq</a> · <b>infrastructure-docs</b></sub></p>

## What's documented

Reference documentation for the homelab Cortex ran on: Proxmox virtualization underneath K3s Kubernetes, segmented into VLANs behind an OPNsense firewall.

<img src="docs/architecture.svg" width="100%" alt="Homelab network: internet, OPNsense firewall, VLANs 140, 145 and 150, Proxmox, the K3s cluster and its services">

| Topic | What's covered |
|---|---|
| [Proxmox](proxmox/) | Hypervisor setup and VM management |
| [Kubernetes](kubernetes/k3s/) | K3s cluster architecture and node configuration |
| [Networking](network/) | VLAN topology and the OPNsense firewall |
| [Services](services/) | Wazuh (SIEM), n8n (automation), Grafana (monitoring) |

---

<p align="center"><sub>Part of the <a href="https://github.com/cortex-io">Cortex archive</a> · built with Claude</sub></p>
