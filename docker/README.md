# 🐳 Docker VM

## VM Specs
- OS: Ubuntu Server 22.04
- CPU: 4 cores
- RAM: 8GB
- Disk: 64GB (local-lvm)
- IP: < DOCKER-VM-IP >

## Services
| Service | Port | Purpose |
|---|---|---|
| Komga | 25600 | Manga and comic server |
| Portainer | 9000 | Docker container management UI |

## Storage
- Comics/Manga mounted from TrueNAS SMB share
- Mount point: `/mnt/comics-manga`
- TrueNAS share: `\\<TRUENAS-IP>\comics-manga`

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

## Komga Docker Compose
```yaml
version: "3"
services:
  komga:
    image: gotson/komga
    container_name: komga
    ports:
      - "25600:25600"
    volumes:
      - /mnt/comics-manga:/comics-manga
      - ./config:/config
    restart: unless-stopped
```

## Portainer Setup
```bash
docker volume create portainer_data
docker run -d \
  -p 9000:9000 \
  --name=portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce
```

## Access
| Service | Local | Tailscale |
|---|---|---|
| Komga | http://< DOCKER-VM-IP >:25600 | http://< DOCKER-TAILSCALE-IP >:25600 |
| Portainer | http://< DOCKER-VM-IP >:9000 | http://< DOCKER-TAILSCALE-IP >:9000 |

## Notes
- SMB share credentials stored in /etc/fstab
- Komga library path set to `/comics-manga`
- Komga stack shows as "Limited" in Portainer (created outside Portainer)
- Files stored on TrueNAS fast pool (2TB NVMe)
