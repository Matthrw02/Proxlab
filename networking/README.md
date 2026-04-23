# 🌐 Networking

## Network Layout
| Device | Local IP | Tailscale IP |
|---|---|---|
| Proxmox | < ROXMOX-IP > | < PROXMOX-TAILSCALE-IP > |
| TrueNAS VM | < TRUENAS-IP > | < TRUENAS-TAILSCALE-IP > |
| Docker VM | < DOCKER-VM-IP > | < DOCKER-VM-TAILSCALE-IP > |

## DNS
- Primary: < ROUTER-IP > (router)

## Tailscale
- Installed on Proxmox, TrueNAS VM and Docker VM
- Allows secure remote access without port forwarding
- All devices accessible via 100.x.x.x addresses

## Remote Access
| Service | Local Access | Remote Access (Tailscale) |
|---|---|---|
| Proxmox UI | https://< PROXMOX-IP >:8006 | https://< PROXMOX-TAILSCALE-IP >:8006 |
| TrueNAS UI | http://< TRUENAS-IP > | http://< TRUENAS-TAILSCALE-IP > |
| Komga | http://< DOCKER-VM-IP >:25600 | http://< DOCKER-VM-TAILSCALE-IP >:25600 |
| Portainer | http://< DOCKER-VM-IP >:9000 | http://< DOCKER-VM-TAILSCALE-IP >:9000 |
| Nginx Proxy Manager | http://< DOCKER-VM-IP >:81 | http://< DOCKER-VM-TAILSCALE-IP >:81 |
| Uptime Kuma | http://< DOCKER-VM-IP >:3001 | http://< DOCKER-VM-TAILSCALE-IP >:3001 |
| Heimdall | http://< DOCKER-VM-IP >:8080 | http://< DOCKER-VM-TAILSCALE-IP >:8080 |

## SMB Share
- Share: `comics-manga`
- Host: TrueNAS VM
- Mount point on Docker VM: `/mnt/comics-manga`

## Domain
- matthrw.com (Cloudflare) — komga.matthrw.com planned

## Future Plans
- komga.matthrw.com via Cloudflare + Nginx Proxy Manager
- Pi-hole for network wide ad blocking and local DNS
- Second Proxmox node (IdeaPad Gaming 3)
- Minecraft and Palworld game servers
