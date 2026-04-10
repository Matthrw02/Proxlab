# 🖥️ ProxLab — Personal Homelab

> Designing and deploying a scalable Proxmox-based homelab.

## Hardware
- HP EliteDesk 805 G6 Mini
- Ryzen 5 4650GE
- 32GB RAM
- 1TB NVMe (Proxmox OS)
- 2TB NVMe (Fast Storage)
- 2TB SATA SSD (Bulk/Backup)

## Architecture
- **Proxmox VE** — Hypervisor managing all VMs
- **TrueNAS Scale VM** — NAS, file storage, SMB shares
- **Docker VM** — Containerized apps (Komga, future services)

## Storage Design
- 2TB NVMe → Primary storage (fast pool) — manga, media, data
- 2TB SATA → Backup pool — ZFS snapshots and replication

## Services
| Service | VM | Purpose |
|---|---|---|
| TrueNAS Scale | TrueNAS VM | File storage + SMB shares |
| Komga | Docker VM | Manga/comic server |

## Future Plans
- Tailscale remote access
- Nginx reverse proxy
- Grafana + Prometheus monitoring
- Automated ZFS backups

## What I Learned
- Hypervisor setup and VM management
- ZFS storage pools and datasets
- NAS configuration and SMB sharing
- Docker containerization
