# Home Network Setup

## Overview
This repository documents the implementation of a **home network setup** with VLAN segmentation, security policies, and network management. The project aims to provide a **scalable, secure, and efficient** networking solution.

## Network Topology
<a href="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Topology.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Topology.jpg" width="600">
</a>

---

## Equipment List
| Device | Purpose | Placement | Notes |
|--------|---------|-----------|-------|
| **Actiontec T3200** | ISP Modem/Router | Bridge Mode | 1Gbps speeds |
| **Ubiquiti Dream Machine Pro** | Gateway, Firewall, DHCP, DNS | Centralized | Remote management |
| **Unifi USW-Lite-8-PoE** | Main switch | Centralized | Tagged VLANs: Secure, IoT, Camera, Guest |
| **UniFi Flex Mini** | IoT Switch | Distributed | VLANs: Secure, IoT |
| **APC UPC 1500 Pro** | Backup Power | Rack | Ensures uptime |

## VLAN Configuration
| VLAN | ID | Subnet | Purpose | Communication |
|------|----|--------|---------|--------------|
| **Management** | 1 | 192.168.10.0/24 | Network Devices | Isolated |
| **Secure** | 20 | 192.168.20.0/24 | Personal Network | Full Access |
| **IoT** | 30 | 192.168.30.0/24 | Smart Home Devices | Internet only, limited LAN |
| **Camera** | 40 | 192.168.40.0/24 | WiFi Security Cameras | Internet only |
| **Guest** | 50 | 192.168.50.0/24 | Guest WiFi | Internet access, casting to IoT |

## Firewall Rules
<a href="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Firewall_rules.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Firewall_rules.jpg" width="600">
</a>

[https://github.com/JoHaa-D/Homelab_Projects/blob/main/network-setup/.images/Firewal_rules.jpg?raw=true](https://github.com/JoHaa-D/Homelab_Projects/blob/main/network-setup/.images/Firewal_rules.jpg?raw=true)

## Wireless Network (SSID Setup)
<a href="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/WIFI_SSID_Network.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/WIFI_SSID_Network.jpg" width="600">
</a>

## Network Management
<a href="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Network_Management.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Network_Management.jpg" width="600">
</a>

## Implementation Details
- **Bridge Mode**: ISP modem/router configured in bridge mode to let **Ubiquiti Dream Machine Pro** handle routing.
- **DHCP & DNS**: Managed via UDM-Pro.
- **IoT VLAN Isolation**: IoT devices cannot communicate with Secure or Guest networks.
- **Guest VLAN**: Provides internet access with limited casting ability.

## Conclusion
This homelab project demonstrates best practices in network segmentation, firewall configurations, and VLAN security for a home environment.
