# CCNA-Packet-Tracer-Labs
A collection of Cisco network topologies and configurations for my CCNA certification journey.
# Lab: Inter-Branch WAN Connectivity (Serial/RIPv2)

## 🎯 Objective
To establish end-to-end connectivity between two geographically separated LANs using Cisco Serial interfaces and the RIPv2 dynamic routing protocol.

## 🛠️ Technologies Used
* **Hardware:** Cisco 2911 Routers, HWIC-2T Serial Modules.
* **Protocols:** RIPv2, DHCP, ICMP.
* **Security:** MD5 Encrypted Enable Secret passwords.
* **WAN:** Serial DCE/DTE with Clocking.

## 🗺️ Topology
![Network Topology](topology.png)

## 🚀 Key Commands Used
### Serial Configuration (Router3 - DCE)
```bash
interface Serial0/3/0
 ip address 10.0.0.1 255.255.255.252
 clock rate 128000
 no shutdown
