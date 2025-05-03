## Hardware Details

- **Hardware**: Intel NUC8 Hades Canyon
- **CPU**: Intel i7 with Radeon RX
- **RAM**: 64GB
- **Storage**: 250GB NVMe SSD (OS) + 1TB NVMe SSD (VMs)

## Network Details

!!! note "Best of both worlds"

    Dual bridge configuration separates domains easily with Proxmox

=== "Main Services"

    * vmbr0 bridge for general infrastructure
    * burp suite
    * aasdfadfs

=== "Security Lab" wordy?

    * vmbr1 for security infrastructure
    * no internet access
    * Windows machines restricted to internal lab network on vmbr1
    * Kali configured to access both networks as pivot point
    * VLAN tagged for ease of access via Proxmox

### 
