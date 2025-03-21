# Home Network Setup - Homelab Project

## Overview
This project documents the implementation of a segmented home network using a Ubiquiti EdgeRouter 4, VLANs, firewall rules, and wireless SSIDs for better security and performance.

### Goals:
- Create separate VLANs for **Personal, IoT, and Guest** devices.
- Implement **firewall rules** to control inter-VLAN traffic.
- Optimize **wireless access points** and SSIDs for segmentation.
- Deploy a **home NAS server** for secure file sharing.

---

## Network Topology
![Network Topology]([network-setup/.images/Topology.jpg](https://github.com/JoHaa-D/Homelab_Projects/blob/main/network-setup/.images/Topology.jpg?raw=true))
> *Diagram of the network layout*

[🔍 Click here to view full size](network-setup/.images/Topology.jpg)

---

## VLAN & Firewall Rules
| VLAN | Purpose | Subnet |
|------|---------|--------|
| **VLAN 10** | Home Network | `192.168.10.0/24` |
| **VLAN 20** | IoT Devices | `192.168.20.0/24` |
| **VLAN 30** | Guest Network | `192.168.30.0/24` |

### Firewall Setup
- **Allow** Home → IoT & Guest
- **Block** IoT → Home & Guest
- **Allow** Guest → IoT
- **Block** Guest → Home

📜 **Firewall Rules Configuration**
![Firewall Rules](network-setup/.images/Firewall_rules.jpg)

[🔍 View Larger](network-setup/.images/Firewall_rules.jpg)

---

## Network Devices
![Devices Connected](network-setup/.images/Network_Devices.JPG)
[🔍 Click to enlarge](network-setup/.images/Network_Devices.JPG)

---

## Wireless SSID Setup
| SSID | VLAN | Frequency |
|------|------|-----------|
| **Home_Network** | VLAN 10 | 5GHz |
| **IoT_Network** | VLAN 20 | 2.4GHz |
| **Guest_Network** | VLAN 30 | 2.4GHz |

📡 **SSID Configuration**
![WiFi Setup](network-setup/.images/WIFI_SSID_Network.jpg)

[🔍 Click for Full View](network-setup/.images/WIFI_SSID_Network.jpg)

---

## Future Improvements:
- **Integrate a NAS server** for family file sharing.
- **Enhance security** by implementing **DNS filtering & VPN access**.
- **Add monitoring & logging** to track network traffic.

---

## How to Contribute
1. Clone the repo:
   ```sh
   git clone https://github.com/JoHaa-D/Homelab_Projects.git
