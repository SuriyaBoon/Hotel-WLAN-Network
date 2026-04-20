# 🏨 Secure Hotel WLAN Network Design & Implementation

![Network](https://img.shields.io/badge/Cisco-Packet%20Tracer-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Score](https://img.shields.io/badge/Portfolio%20Score-9%2F10-gold)
![Version](https://img.shields.io/badge/Version-2.0-informational)

## 📋 Overview

A comprehensive enterprise-grade hotel network infrastructure designed and implemented in Cisco Packet Tracer. This project demonstrates real-world network design principles including redundancy, security, VoIP, wireless management, and dynamic routing.

The network supports **3,400+ concurrent users** across a Guest Block (6 floors) and Employee Block with full internet connectivity, VoIP telephony, and wireless access.

---

## 🗺️ Network Topology

```
Internet
    │
[INTERNET-ROUTER]
    │
[OUTSIDE-SW1/SW2] (3650-24PS x2 - Full Mesh)
    │
[PERIMETER-FIREWALL 1/2/3] (ASA 5506-X x3)
    │
[INSIDE-SW1/SW2] (3650-24PS x2 - Full Mesh)
    │
[COREROUTER1/2] (2811 x2 - OSPF)
    │
[BLOCK-A-MLSW1/2] (3650-24PS x2 - HSRP + LACP)
    ├── [SERVER FARM] (DC-SWITCH)
    ├── [GUEST BLOCK] (Ground Floor + Floor 1-5)
    └── [EMPLOYEE BLOCK]
```

---

## ✅ Features Implemented

### Network Infrastructure
| Feature | Technology | Status |
|---------|-----------|--------|
| Multi-Layer Architecture | Hierarchical Design | ✅ |
| Dynamic Routing | OSPF Area 0 | ✅ |
| Gateway Redundancy | HSRP Active/Standby | ✅ |
| Link Aggregation | LACP EtherChannel | ✅ |
| Traffic Segmentation | VLANs (9 VLANs) | ✅ |
| Internet Connectivity | NAT + Static Routing | ✅ |

### Security
| Feature | Technology | Status |
|---------|-----------|--------|
| Perimeter Security | Cisco ASA Firewall x3 | ✅ |
| NAT | Dynamic PAT | ✅ |
| Traffic Control | Extended ACL | ✅ |
| Access Control | Switch Port Security | ✅ |
| Remote Management | SSH v2 | ✅ |
| Password Protection | Enable Secret + Encryption | ✅ |
| Wireless Security | WPA2-AES | ✅ |

### Services
| Feature | Technology | Status |
|---------|-----------|--------|
| IP Management | DHCP + DHCP Relay | ✅ |
| Name Resolution | DNS (hotel.com) | ✅ |
| Email | SMTP/POP3 | ✅ |
| Web | HTTP/HTTPS | ✅ |
| VoIP | Cisco CME (1001-1020) | ✅ |
| Wireless | WLC-2504 + 18 APs | ✅ |
| Time Sync | NTP | ✅ |
| Log Management | Syslog | ✅ |
| Voice QoS | DSCP EF + mls qos | ✅ |

---

## 🌐 IP Addressing Scheme

| Zone | Network | Purpose |
|------|---------|---------|
| ISP Links | 200.100.50.0/24 | WAN Connectivity |
| DMZ Outside | 200.100.50.44-74/30 | Firewall Outside |
| DMZ Inside | 10.10.4.0/22 | Internal Core |
| VLAN 10 (Guest F1) | 10.10.28.0/23 | Floor 1 Guests |
| VLAN 20 (Guest F2) | 10.10.30.0/23 | Floor 2 Guests |
| VLAN 30 (Guest F3) | 10.10.32.0/23 | Floor 3 Guests |
| VLAN 40 (Guest F4) | 10.10.34.0/23 | Floor 4 Guests |
| VLAN 50 (Guest F5) | 10.10.36.0/23 | Floor 5 Guests |
| VLAN 55 (Employee) | 10.10.20.0/23 | Staff Network |
| VLAN 60 (Ground) | 10.10.38.0/23 | Ground Floor |
| VLAN 99 (VoIP) | 172.16.10.0/16 | IP Phones |
| VLAN 199 (Server) | 10.10.1.224/27 | Server Farm |

---

## 🔧 Technologies Used

- **Routing**: OSPF Area 0, Static Routes
- **Switching**: VLANs, STP PortFast, Trunk Links
- **Redundancy**: HSRP, LACP EtherChannel, Dual Uplinks
- **Security**: ASA Firewall, NAT, ACL, Port Security, SSH v2, WPA2
- **Wireless**: Cisco WLC-2504, Autonomous AP, LAP-PT
- **VoIP**: Cisco CME, IP Phone 7960, DHCP Option 150
- **Services**: DHCP, DNS, HTTP, SMTP/POP3, NTP, Syslog
- **QoS**: DSCP EF, mls qos trust dscp

---

## 📁 Repository Structure

```
Hotel-WLAN-Network/
├── README.md
├── Hotel_Network.pkt          # Cisco Packet Tracer File
├── docs/
│   ├── Hotel_Network_Manual_v2.docx    # Network Manual
│   └── Hotel_Network_Configs_v2.docx  # Device Configurations
└── screenshots/
    ├── topology_overview.png
    ├── server_farm.png
    ├── guest_block.png
    └── employee_block.png
```

---

## 🚀 How to Open

1. Install **Cisco Packet Tracer** (version 8.0+)
2. Download `Hotel_Network.pkt`
3. Open file in Packet Tracer
4. Wait for network to converge (~30 seconds)
5. Test connectivity using simulation mode

---

## 🧪 Test Cases

| Test | Command | Expected Result |
|------|---------|----------------|
| Internet User | `ping 192.168.10.1` from Internet PC | Success |
| Guest Web | Browser → `http://hotel.com` | Cisco PT Page |
| Guest Email | Send email guest1@hotel.com | Delivered |
| VoIP Call | Dial 1002 from IP Phone 1001 | Connected |
| DHCP | IP Configuration → DHCP | Gets IP |
| SSH | `ssh admin@[device_ip]` | Login Prompt |
| Guest→Employee Block | `ping 10.10.20.x` from Guest | Blocked (ACL) |

---

## 📊 High Availability Design

```
Every layer has redundancy:

ISP Layer:      ISP-R1 (primary) → ISP-R2 (secondary) → ISP-R3 (tertiary)
Firewall:       FW-1 || FW-2 || FW-3 (parallel)
Core Router:    CR1 (OSPF) ←→ CR2 (OSPF)
Distribution:   MLSW1 (HSRP Active) ←LACP→ MLSW2 (HSRP Standby)
Access:         Each switch has dual uplinks to MLSW1 and MLSW2
```

---

## 📝 Device Credentials

> ⚠️ For lab purposes only. Change in production environment.

| Access | Username | Password |
|--------|---------|---------|
| SSH/VTY | admin | Cisco@123 |
| Console | - | Cisco@123 |
| Enable | - | Cisco@123 |
| WLC GUI | admin | Cisco@123 |
| Wireless | - | Cisco@123 |

---

## 👨‍💻 Skills Demonstrated

- Enterprise Network Design
- Cisco IOS Configuration
- Network Security Implementation
- VoIP Deployment
- Wireless Network Management
- Network Documentation
- Troubleshooting Methodology

---

## 📄 License

This project is for educational and portfolio purposes.

---

*Built with Cisco Packet Tracer | April 2026*
