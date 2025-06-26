# 🏪 Small Business Network Plan

## 📘 Overview

This project simulates a scalable network infrastructure for a small café. The setup includes secure segmentation between staff devices (POS systems, Admin PCs) and public guest Wi-Fi using VLANs and a wireless access point. Built using Cisco Packet Tracer to demonstrate real-world networking design and security considerations.

---

## 🗺️ Network Topology

![Network Diagram](https://i.imgur.com/0k264m4.png)


---

## 🧩 IP Addressing Scheme

| VLAN | Purpose         | IP Range         | Devices                      |
|------|------------------|------------------|------------------------------|
| 10   | Staff Network    | 192.168.10.0/24  | POS1, POS2, AdminPC          |
| 20   | Guest Wi-Fi      | 192.168.20.0/24  | Wireless Clients             |
| WAN  | ISP Link         | 203.0.113.2/30   | Router G0/0                  |

**DHCP**: Enabled for VLAN 20 via WRT300N or Router  
**Static IPs**: Used for VLAN 10 staff devices

---

## 🔐 VLAN & Security Configuration

- **VLAN 10**: For internal POS and Admin devices  
- **VLAN 20**: For isolated Guest Wi-Fi access  
- **Router-on-a-stick**: Used to enable inter-VLAN routing  
- **WPA2-PSK Security** on Guest Wi-Fi (SSID: `CafeGuest`, Pass: `coffee2025`)  
- **ACLs**: Block traffic between VLAN 20 and VLAN 10

---

## ⚙️ Sample Configuration Snippets

interface Gig0/0
ip address 203.0.113.2 255.255.255.252
no shutdown

interface Gig0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface Gig0/1.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

ip access-list extended BLOCK-GUEST
deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
permit ip any any

---

## 🧠 What I Learned
Network segmentation using VLANs for secure design

Configuring router-on-a-stick and trunk ports

Securing public wireless access and isolating traffic

IP planning for small business use cases

---

## 🚀 Future Enhancements
Add NAT for internet access simulation

Configure SNMP for monitoring

Create guest portal authentication for Wi-Fi
