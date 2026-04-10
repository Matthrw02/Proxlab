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
| fast | 2TB NVMe | 1.8T | Primary storage |
| bulk | 2TB SATA | 1.7T | Backup + snapshots |

## Datasets
| Dataset | Path | Purpose |
|---|---|---|
| comics-manga | /mnt/fast/comics-manga | Manga and comic storage |

## SMB Shares
| Share | Path |
|---|---|
| comics-manga | /mnt/fast/comics-manga |

## Notes
- Drives passed through from Proxmox as raw disks
- Duplicate serial number issue fixed using custom serials in qm set
- ZFS replication from fast → bulk planned
