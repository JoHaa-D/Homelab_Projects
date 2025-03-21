# Home Network Setup

## Overview
This repository documents the implementation of a **home network setup** with VLAN segmentation, security policies, and network management. The project aims to provide a **scalable, secure, and efficient** networking solution.

## Network Topology
[![Network Topology](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Topology.jpg)](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Topology.jpg)
Click the image for a larger view:


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
![Firewall Rules](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Firewall_rules.jpg)
[Click to enlarge](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Firewall_rules.jpg)

## Wireless Network (SSID Setup)
![WiFi SSID Network](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/WIFI_SSID_Network.jpg)
[Click to enlarge](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/WIFI_SSID_Network.jpg)

## Network Management
![Network Management](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Network_Management.jpg)
[Click to enlarge](https://raw.githubusercontent.com/JoHaa-D/Homelab_Projects/main/network-setup/.images/Network_Management.jpg)

## Implementation Details
- **Bridge Mode**: ISP modem/router configured in bridge mode to let **Ubiquiti Dream Machine Pro** handle routing.
- **DHCP & DNS**: Managed via UDM-Pro.
- **IoT VLAN Isolation**: IoT devices cannot communicate with Secure or Guest networks.
- **Guest VLAN**: Provides internet access with limited casting ability.

## Conclusion
This homelab project demonstrates best practices in network segmentation, firewall configurations, and VLAN security for a home environment.
