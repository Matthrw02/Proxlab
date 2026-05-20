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
- **Docker VM** — Containerized apps (Komga, Nextcloud, supporting services)

## Storage Design
- 2TB NVMe → Primary storage (Fast pool) — manga, Nextcloud data
- 2TB SATA → Backup pool — ZFS snapshots and weekly replication

## Services
| Service | VM | Purpose |
|---|---|---|
| TrueNAS Scale | TrueNAS VM | File storage + SMB shares |
| Komga | Docker VM | Manga/comic server |
| Nextcloud | Docker VM | Self-hosted file sync, photo backup, Google Drive replacement |
| Nginx Proxy Manager | Docker VM | Reverse proxy |
| Uptime Kuma | Docker VM | Service monitoring |
| Heimdall | Docker VM | Homelab dashboard |
| Portainer | Docker VM | Docker management UI |
| Watchtower | Docker VM | Automatic container updates |

## Remote Access
- Tailscale on Proxmox, TrueNAS VM, and Docker VM
- Cloudflare Tunnel for public-facing services (Komga at komga.apple.com)
- Domain: `apple.com` (managed via Cloudflare)

## Future Plans
- Cloudflare Tunnel for Nextcloud (cloud.apple.com)
- Grafana + Prometheus monitoring
- LearnLab build (separate hardware) — AD → Azure/Entra ID → Kubernetes

## What I Learned
- Hypervisor setup and VM management
- ZFS storage pools, datasets, and replication
- NAS configuration and SMB sharing
- Docker containerization and stack management via Portainer
- Self-hosted alternatives to commercial cloud services
- SMB mount permissions and uid/gid mapping into containers
