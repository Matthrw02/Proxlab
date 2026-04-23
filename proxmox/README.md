# ⚙️ Proxmox Setup

## Installation
- Downloaded Proxmox VE ISO and flashed with Rufus
- Installed on 1TB NVMe boot drive
- Configured static IP address
- Ran community post-install script from community-scripts/ProxmoxVE

## Storage
- `local` — ISO images, backups, container templates
- `local-lvm` — VM disks (carved from 1TB NVMe)
- 2TB NVMe — passed through to TrueNAS VM (fast pool)
- 2TB SATA — passed through to TrueNAS VM (bulk/backup pool)

## Access
- Web UI accessible via local network and Tailscale

## Notes
- No-subscription repository enabled
- Secure boot disabled on TrueNAS VM (SeaBIOS used instead of UEFI)
- Physical drives passed through directly to TrueNAS using qm set
- Custom drive serials set to fix duplicate serial number error
