# Infrastructure

## Origins

My homelab was originally built to provide myself with access to multimedia services such as yt-dlp. 

I wanted a quick way to access these services so I implemented pi-hole for DNS and ad blocking.

I then implemented an internal NGINX forward proxy for simple port forwarding. This allows me to access an internal service with easily customizable URL redirects such as: dlp.lab, proxmox.lab, etc

NGINX requires an SSL certificate for such redirects. Since this is a lab/internal environment, I chose to self help a PKI by way of 'step-ca'

- Pi Hole
- NGINX Proxy Manager
- Step-ca

## Overview

#### Hardware Details

- **Hardware**: Intel NUC8 Hades Canyon
- **CPU**: Intel i7 with Radeon RX
- **RAM**: 64GB
- **Storage**: 250GB NVMe SSD (OS) + 1TB NVMe SSD (VMs)

#### Network Details

!!! note "Best of both worlds"

    Dual bridge configuration separates domains easily with Proxmox

=== "Main Services"

    * vmbr0 bridge for general infrastructure
    * burp suite
    * aasdfadfs

=== "Security Lab"

    * vmbr1 for security infrastructure
    * no internet access
    * Windows machines restricted to internal lab network on vmbr1
    * Kali configured to access both networks as pivot point
    * VLAN tagged for ease of access via Proxmox



![nuc8](/Users/ranger/dev/mkdocsmaterial/docs/assets/nuc8.jpg)

