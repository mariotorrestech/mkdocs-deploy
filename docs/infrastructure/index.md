---
title: Infrastructure

---

# Infrastructure Overview

## Origins & Purpose

Originally built for multimedia services access (yt-dlp), evolved into a comprehensive security lab environment with core services:

- Pi-Hole (DNS and ad blocking)
- NGINX Forward Proxy (internal service access)
- Step-CA (internal PKI for SSL certificates)

## Hardware Details

- **System**: Intel NUC8 Hades Canyon
- **CPU**: Intel i7 with Radeon RX
- **RAM**: 64GB
- **Storage**: 250GB NVMe SSD (OS) + 1TB NVMe SSD (VMs)

## Network Configuration

Dual bridge configuration separates domains:

- vmbr0 bridge for general infrastructure
- vmbr1 for security infrastructure
  - No internet access
  - Windows machines restricted to internal lab network
  - Kali configured as pivot point between networks
  - VLAN tagged for Proxmox management

## Lab Environments

- [Active Directory Lab](ActiveDirectoryLab.md)
- [Web Application Lab](WebAppLab.md)
- [Network Details](network.md)

![Intel NUC8](../assets/nuc8.jpg)


---

*Return to [Home](../index.md)*