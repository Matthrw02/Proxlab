## 🐳 Docker VM

## VM Specs
- OS: Ubuntu Server 22.04
- CPU: 4 cores
- RAM: 8GB
- Disk: 64GB (local-lvm)
- IP: <DOCKER-VM-IP>

## Services
| Service | Port | Purpose |
|---|---|---|
| Komga | 25600 | Manga and comic server |
| Nextcloud | 8081 | Self-hosted file storage, sync, and phone backup |
| Portainer | 9000 | Docker container management UI |
| Nginx Proxy Manager | 81 | Reverse proxy |
| Uptime Kuma | 3001 | Service monitoring |
| Watchtower | - | Automatic weekly container updates |
| Heimdall | 8080 | Homelab dashboard |

## Storage
- Comics/Manga mounted from TrueNAS SMB share at `/mnt/comics-manga`
- Nextcloud data mounted from TrueNAS SMB share at `/mnt/nextcloud-data`

## Setup Commands
```bash
# Install Docker
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER

# Install SMB client
sudo apt install cifs-utils smbclient -y

# Create mount points
sudo mkdir /mnt/comics-manga
sudo mkdir /mnt/nextcloud-data

# Make mounts permanent (add to /etc/fstab)
//TRUENAS-IP/comics-manga    /mnt/comics-manga    cifs username=smbuser,password=...,uid=1000,gid=1000 0 0
//TRUENAS-IP/nextcloud-data  /mnt/nextcloud-data  cifs username=smbuser,password=...,uid=33,gid=33,file_mode=0770,dir_mode=0770 0 0
```

## Nextcloud Stack
Deployed via Portainer. Includes Nextcloud + MariaDB + Redis.

```yaml
version: "3"

services:
  nextcloud-db:
    image: mariadb:10.11
    container_name: nextcloud-db
    restart: unless-stopped
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    environment:
      - MYSQL_ROOT_PASSWORD=< REDACTED >
      - MYSQL_PASSWORD=< REDACTED >
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
    volumes:
      - nextcloud-db:/var/lib/mysql

  nextcloud-redis:
    image: redis:alpine
    container_name: nextcloud-redis
    restart: unless-stopped

  nextcloud:
    image: nextcloud:latest
    container_name: nextcloud
    restart: unless-stopped
    ports:
      - "8081:80"
    depends_on:
      - nextcloud-db
      - nextcloud-redis
    environment:
      - MYSQL_HOST=nextcloud-db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=< REDACTED >
      - REDIS_HOST=nextcloud-redis
      - NEXTCLOUD_TRUSTED_DOMAINS=< DOCKER-VM-IP > < DOCKER-VM-TAILSCALE-IP >
    volumes:
      - nextcloud-config:/var/www/html
      - /mnt/nextcloud-data:/var/www/html/data

volumes:
  nextcloud-db:
  nextcloud-config:
```

## Notes
- All containers deployed and managed via Portainer
- Nextcloud SMB mount uses `uid=33,gid=33` (www-data inside container) with `0770` perms
- Nextcloud trusted_domains includes local IP, Tailscale IP, and cloud.matthrw.com (future tunnel)
- Komga SMB mount uses `uid=1000,gid=1000` (user)
- Watchtower runs every Sunday at 4am
- SMB credentials stored in /etc/fstab
