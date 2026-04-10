# 🌐 Networking

## Network Layout
| Device | Local IP | Tailscale IP |
|---|---|---|
| Proxmox | < PROXMOX-IP > | < PROXMOX-TAILSCALE-IP > |
| TrueNAS VM | < TRUENAS-IP > | < TRUENAS-TAILSCALE-IP > |
| Docker VM | < DOCKER-VM-IP > | < DOCKER-VM-TAILSCALE-IP > |

## DNS
- Primary: <ROUTER-IP> (router)

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

## SMB Share
- Share: `comics-manga`
- Host: TrueNAS VM
- Mount point on Docker VM: `/mnt/comics-manga`

## Future Plans
- Nginx Proxy Manager for clean local URLs
- Pi-hole or AdGuard for local DNS
- Second Proxmox node (ThinkPad X1 Carbon Gen 9)
- Minecraft and Palworld game servers
