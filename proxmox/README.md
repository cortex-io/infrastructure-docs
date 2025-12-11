# Proxmox Infrastructure

## Nodes

### pve02 (Main)

| Property | Value |
|----------|-------|
| IP | 10.88.140.164 |
| Web UI | https://10.88.140.164:8006 |
| OS | Proxmox VE 8.x |

## Virtual Machines

| VMID | Name | IP | Specs | Purpose |
|------|------|-----|-------|---------|
| 201 | wazuh-server | 10.88.140.202 | 4 vCPU, 8GB RAM, 100GB | Wazuh SIEM |

## LXC Containers

| CTID | Name | IP | Specs | Purpose |
|------|------|-----|-------|---------|
| 100 | claude-vm | 10.88.140.252 | - | Claude agent VM |
| 300 | k3s-master | 10.88.145.170 | 4 vCPU, 8GB RAM | k3s server node |
| 301 | k3s-worker-1 | 10.88.145.171 | 4 vCPU, 8GB RAM | k3s agent node |
| 302 | k3s-worker-2 | 10.88.145.172 | 4 vCPU, 8GB RAM | k3s agent node |

## Network Bridges

| Bridge | VLAN | Subnet | Gateway | Purpose |
|--------|------|--------|---------|---------|
| vmbr0 | 140 | 10.88.140.0/24 | 10.88.140.1 | Default network |
| vmbr1 | 145 | 10.88.145.0/24 | 10.88.145.1 | k3s/Kubernetes |

## Storage

| Storage | Type | Path | Purpose |
|---------|------|------|---------|
| local | dir | /var/lib/vz | ISOs, templates |
| local-lvm | LVM | - | VM disks |

## Common Commands

```bash
# SSH to Proxmox
ssh root@10.88.140.164

# Execute command in LXC
pct exec 300 -- <command>

# Start/Stop container
pct start 300
pct stop 300

# Container console
pct enter 300

# List containers
pct list

# VM commands
qm start 201
qm stop 201
qm list
```
