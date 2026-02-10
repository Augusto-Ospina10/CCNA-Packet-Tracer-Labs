# Full-Stack Branch Connectivity Lab: DHCP, Serial WAN, & RIPv2

## 🎯 Project Objective
The goal of this project was to design and implement a complete network infrastructure for two geographically separated branch offices. This lab demonstrates mastery over local network services (DHCP), hardware modularity (Serial), and dynamic routing (RIPv2).

---

## 🏗️ Implementation Phases

### Phase 1: LAN Foundation & Local Services
Established the local office "islands" to ensure host stability and automated addressing before WAN integration.
* **Default Gateway Setup:** Configured GigabitEthernet 0/0 interfaces on Cisco 2911 routers to serve as the exit point for the 192.168.1.0/24 and 192.168.2.0/24 networks.
* **DHCP Server Configuration:** Instead of static IPs, I configured each router as a DHCP server to automatically assign IP addresses, subnet masks, and default gateway information to all PCs.
* **Verification:** Tested local host-to-gateway connectivity to ensure the LAN was operational.

### Phase 2: WAN & Physical Interconnect
Physically and logically bridged the two branch routers.
* **Hardware Provisioning:** Installed **HWIC-2T** high-speed serial cards into the physical chassis of the Cisco 2911 routers.
* **DCE/DTE Synchronization:** Identified the **DCE** end of the serial cable using the `show controllers` command and applied a `clock rate 128000` to synchronize bit-timing.
* **WAN Subnetting:** Configured a point-to-point **/30** subnet (10.0.0.0/30) on the serial interfaces to maximize IP address efficiency.

### Phase 3: Dynamic Routing & Security
Enabled "End-to-End" communication and hardened the devices for administrative access.
* **Routing Protocol:** Implemented **RIP Version 2** with the `no auto-summary` command, allowing routers to exchange specific subnet masks across the serial link.
* **Administrative Hardening:** Secured the "Privileged EXEC" mode using the `enable secret` command (MD5 hashing) to protect the router configuration.

---

## 🗺️ Topology Diagram
![Network Topology](topology.png)

---

## 🚀 Key Configurations & CLI Snippets

### 1. DHCP Pool Setup (Automating the LAN)
```bash
ip dhcp pool BRANCH_OFFICE
 network 192.168.x.0 255.255.255.0
 default-router 192.168.x.1
 dns-server 8.8.8.8
2. Serial WAN Configuration (The Physical Link)
Bash
interface Serial0/3/0
 ip address 10.0.0.x 255.255.255.252
 clock rate 128000
 no shutdown
3. RIPv2 Setup (The Logical Bridge)
Bash
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 192.168.x.0
