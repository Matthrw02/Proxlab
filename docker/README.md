# 🐳 Docker VM

## VM Specs
- OS: Ubuntu Server 22.04
- CPU: 4 cores
- RAM: 8GB
- Disk: 64GB (local-lvm)

## Services
| Service | Port | Purpose |
|---|---|---|
| Komga | 25600 | Manga and comic server |
| Portainer | 9000 | Docker container management UI |
| Nginx Proxy Manager | 81 | Reverse proxy + clean URLs |
| Uptime Kuma | 3001 | Service uptime monitoring |
| Watchtower | - | Automatic weekly container updates |
| Heimdall | 8080 | Homelab dashboard |

## Storage
- Comics/Manga mounted from TrueNAS SMB share
- Mount point: `/mnt/comics-manga`

## Setup Commands
```bash
# Install Docker
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER

# Install SMB client and mount TrueNAS share
sudo apt install cifs-utils smbclient -y
sudo mkdir /mnt/comics-manga

# Make mount permanent
echo "//TRUENAS-IP/comics-manga /mnt/comics-manga cifs username=smbuser,uid=1000,gid=1000 0 0" | sudo tee -a /etc/fstab
```

## Notes
- All containers deployed and managed via Portainer
- Komga stack shows as "Limited" in Portainer (created outside Portainer)
- Watchtower runs every Sunday at 4am
- SMB share credentials stored in /etc/fstab
- Files stored on TrueNAS fast pool (2TB NVMe)
