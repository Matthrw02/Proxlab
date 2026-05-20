# 🗄️ TrueNAS Scale Setup

## VM Specs
- OS: TrueNAS Scale 25.10
- CPU: 4 cores
- RAM: 8GB
- Boot disk: 64GB (local-lvm)
- IP: < TRUENAS-IP >

## Storage Pools
| Pool | Drive | Size | Purpose |
|---|---|---|---|
| Fast | 2TB NVMe | 1.8T | Primary storage |
| bulk | 2TB SATA | 1.7T | Backup + snapshots |

## Datasets
| Dataset | Path | Purpose |
|---|---|---|
| comics-manga | /mnt/Fast/comics-manga | Manga and comic storage |
| nextcloud-data | /mnt/Fast/nextcloud-data | Nextcloud user data (files, photos, sync) |

## SMB Shares
| Share | Path | Consumer |
|---|---|---|
| comics-manga | /mnt/Fast/comics-manga | Komga (Docker VM) |
| nextcloud-data | /mnt/Fast/nextcloud-data | Nextcloud (Docker VM) |

## SMB User
- Username: `smbuser`
- Owns both shares with Full Control via NFSv4 ACL

## Notes
- Drives passed through from Proxmox as raw block devices
- Pool name is `Fast` (capital F) — case-sensitive in mount paths
- All datasets are flat (no nesting) — nested ZFS datasets are not visible through parent SMB/NFS exports
- SSH disabled by default — use Web UI Shell for any CLI work
- Weekly ZFS replication: Fast → bulk
