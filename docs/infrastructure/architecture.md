# Infrastructure Architecture

## Overview
My homelab hosts security testing environments including an Active Directory environment and OWASP Juice Shop, with a Kali VM to attack and analyze the two. It also provides core infrastructure services including DNS (Pi-hole), PKI (Step-CA), and NGINX reverse proxy management, along with personal services for notes, budgeting, and media. All of this runs on a compact, energy-efficient NUC platform.

## Hardware Platform
<img src="/images/nuc8.jpg" style="width: 500px; max-width: 100%;" alt="Image of the Hades Canyon homelab">

### Proxmox Host
- **Hardware**: Intel NUC8 Hades Canyon
- **CPU**: Intel i7 8809G with Radeon RX Vega graphics
  - Notable as the first-ever partnership between AMD and Intel on the same silicon
- **RAM**: 64GB DDR4
- **Storage**: 250GB NVMe SSD (OS) + 1TB NVMe SSD (VMs)
- **Network**: Connected to the Unifi switch on a dedicated VLAN, with dual NIC capability (currently using single connection)

### Virtualization Strategy
My Proxmox implementation balances security, flexibility, and resource efficiency:

**Virtualization Hierarchy**:

  - LXC container space: 100-199 for core infrastructure and personal services (Pi-hole, NGINX Proxy Manager, Docker)
    - Full VM virtualization (200+) for security labs, Windows environments, and penetration testing tools in Kali
     - Consistent numbering convention for clarity between use cases

**Network Isolation**:

  - Dual-bridge configuration separating security domains
    - Main services on vmbr0 (192.168.0.0/24) for general infrastructure
    - Isolated AD security lab on vmbr1 (10.10.200.0/24) with no internet access
        - Windows machines restricted to internal lab network only
        - Kali Linux configured as pivot point with access to both networks
        - VLAN tag 200 for additional AD lab isolation

**Storage Implementation**:

  - Dual NVMe SSD configuration with strategic workload distribution:
    - 250GB NVMe primary drive hosts OS and critical infrastructure containers
    - 1TB NVMe secondary drive provides expanded capacity for lab environments
  - Multi-pool thin provisioning strategy:
    - Infrastructure containers (100-series) primarily on system NVMe for performance
    - Lab environments (200-series) with larger allocations on dedicated 1TB storage
    - Overall low storage utilization (54% on system drive, only 2.6% on lab storage) enabling future expansion
  - Resource-appropriate allocation with:
    - Lightweight containers (2-8GB each) for infrastructure services
    - Larger allocations (32-60GB) for Windows VMs and security testing environments
  - Multi-disk configuration for select VMs allowing separation of OS and data

**Automation and Community**:

  - Proxmox community scripts for simplified deployment: [PVE Community Scripts](https://community-scripts.github.io/ProxmoxVE/scripts)
  - Standardized container configurations for reproducibility

## System Architecture Diagram

<img src="/images/homelab-diagram.svg" style="width: 500px; max-width: 100%;" alt="Image of the Hades Canyon homelab">

## Resource Allocation

| Category | Total VMs/LXCs | RAM | Primary Purpose |
|----------|----------------|-----|----------------|
| Infrastructure | 3 | 3GB | [Infrastructure services](../infrastructure/core-services.md) |
| Personal | 5 | 6GB | [Personal services](../infrastructure/personal-services.md) |
| AD and Kali | 4 | 36GB | [Security testing lab](../labs/ad-environment.md) |

---

*Documentation built with MkDocs.*