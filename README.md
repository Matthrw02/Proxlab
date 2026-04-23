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
- **Docker VM** — Containerized apps and services

## Storage Design
- 2TB NVMe → Primary storage (fast pool)
- 2TB SATA → Backup pool (weekly ZFS replication)

## Services
| Service | VM | Purpose |
|---|---|---|
| TrueNAS Scale | TrueNAS VM | File storage + SMB shares |
| Komga | Docker VM | Manga and comic server |
| Portainer | Docker VM | Container management UI |
| Nginx Proxy Manager | Docker VM | Reverse proxy + clean URLs |
| Uptime Kuma | Docker VM | Service monitoring |
| Watchtower | Docker VM | Auto container updates |
| Heimdall | Docker VM | Homelab dashboard |

## Networking
- Tailscale VPN on all VMs and host
- Remote access via Tailscale on all services
- Domain: matthrw.com (Cloudflare) — planned

## Future Plans
- komga.matthrw.com via Cloudflare + Nginx
- Immich photo server
- Pi 4 → Pi-hole + Grafana monitoring
- IdeaPad Gaming 3 → Proxmox node 2
- Minecraft + Palworld game servers
- Dedicated NAS hardware (long term)

## What I Learned
- Hypervisor setup and VM management
- ZFS storage pools, datasets and replication
- NAS configuration and SMB sharing
- Docker containerization and orchestration
- Reverse proxy and networking
- Remote access with Tailscale
