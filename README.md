# 🌐 Full-Stack Branch Connectivity Lab  
**DHCP · Serial WAN · RIPv2**

## 🎯 Project Objective
The goal of this project was to design and implement a complete network infrastructure for two geographically separated branch offices. This lab demonstrates mastery of local network services (DHCP), hardware modularity (Serial WAN), and dynamic routing (RIPv2).

---

## 🏗️ Implementation Phases

### 🔹 Phase 1: LAN Foundation & Local Services
Established stable local networks before integrating the WAN.

- Configured `GigabitEthernet0/0` on Cisco 2911 routers as default gateways for:
  - `192.168.1.0/24`
  - `192.168.2.0/24`
- Configured each router as a DHCP server to automatically assign:
  - IP address
  - Subnet mask
  - Default gateway
  - DNS server
- Verified local connectivity using `ping`

---

### 🔹 Phase 2: WAN & Physical Interconnect
Connected the two branch offices using a serial point-to-point WAN link.

- Installed **HWIC-2T** serial modules on Cisco 2911 routers
- Identified the **DCE** interface using:
  ```bash
  show controllers serial
Applied clocking on the DCE side:

clock rate 128000
Configured a /30 subnet (10.0.0.0/30) to optimize IP usage

🔹 Phase 3: Dynamic Routing & Security
Enabled end-to-end communication and secured administrative access.

Implemented RIPv2 with classless routing:

no auto-summary
Secured privileged EXEC mode using:

enable secret
🗺️ Network Topology


🚀 Key Configurations & CLI Snippets
📌 DHCP Configuration
ip dhcp excluded-address 192.168.1.1 192.168.1.10

ip dhcp pool BRANCH_1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
ip dhcp excluded-address 192.168.2.1 192.168.2.10

ip dhcp pool BRANCH_2
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
 dns-server 8.8.8.8
📌 Serial WAN Configuration
interface Serial0/3/0
 ip address 10.0.0.1 255.255.255.252
 clock rate 128000
 no shutdown
interface Serial0/3/0
 ip address 10.0.0.2 255.255.255.252
 no shutdown
📌 RIPv2 Configuration
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 192.168.1.0
 network 192.168.2.0
✅ Results
DHCP successfully assigns IP configurations to LAN hosts

Serial WAN link operational between branch routers

Dynamic routing enables full inter-branch communication

Routers secured with encrypted privileged access

🧠 Skills Demonstrated
Cisco IOS CLI

DHCP server configuration

Serial WAN setup (DCE/DTE)

Subnetting (/24 and /30)

Dynamic routing with RIPv2

Network verification and troubleshooting
