# 🧠 Proxmox Homelab (Enterprise-Style Setup)

## 📌 Overview

This project documents the design and deployment of a personal homelab built using Proxmox VE on a HP EliteDesk 805 G6. The goal is to simulate a real-world IT infrastructure environment with virtualization, containerization, and centralized services.

## ⚙️ Hardware

* HP EliteDesk 805 G6 Mini
* Ryzen 5 4650GE
* 32GB RAM
* 1TB NVMe (Proxmox OS)
* 2TB NVMe (Fast Storage)
* 2TB SATA SSD (Bulk Storage)

## 🧱 Architecture

* Proxmox VE (Hypervisor)
* Ubuntu VM (Docker Host)
* Services:

  * Komga (Media server)
  * Tailscale (Remote access)

## 💾 Storage Design

* NVMe (Fast): VM disks, databases
* SATA (Bulk): media, files, backups

## 🌐 Networking

* Static IP configuration
* Local DNS via router
* Secure remote access using Tailscale

## 🚀 Key Features

* Virtualized infrastructure using Proxmox
* Containerized applications using Docker
* Secure remote access without port forwarding
* Scalable architecture for future services

## 📈 Future Improvements

* Reverse proxy (Nginx Proxy Manager)
* Automated backups
* ZFS storage implementation
* Kubernetes (long-term goal)

## 📸 Architecture Diagram

*(Add later)*

## 🧠 What I Learned

* Virtualization and hypervisors
* Storage planning and performance optimization
* Networking and remote access setup
* Service deployment and containerization

---
