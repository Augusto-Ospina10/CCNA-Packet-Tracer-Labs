# Full-Stack Branch Connectivity Lab (DHCP, Serial WAN, & RIPv2)

## 🎯 Project Objective
To design and implement a complete network infrastructure for two separate branch offices. This project demonstrates the entire lifecycle of a network build: from local infrastructure services (DHCP) to inter-site connectivity using Serial WAN links and dynamic routing protocols.

---

## 🏗️ Implementation Phases

### Phase 1: LAN Foundation & DHCP Services
Established local connectivity and automated host addressing.
* **Gateway Setup:** Configured GigabitEthernet interfaces on Cisco 2911 routers to serve as the default gateways.
* **Automated Addressing:** Implemented **Cisco IOS DHCP Pools** to dynamically assign IP addresses, masks, and gateways to end-hosts, ensuring a scalable and error-free deployment.

### Phase 2: WAN & Physical Interconnect
Physically and logically bridged the two branch offices across a Wide Area Network.
* **Hardware:** Provisioned **HWIC-2T** high-speed serial cards into the router chassis.
* **Link Sync:** Identified the **DCE** side of the serial cable and applied a `clock rate` of 128000 for bit-timing synchronization.
* **Addressing:** Utilized an efficient `/30` (255.255.255.252) subnet for the point-to-point serial link to conserve IP address space.

### Phase 3: Dynamic Routing & Security
Enabled end-to-end communication and hardened the device management plane.
* **Routing:** Configured **RIPv2** with `no auto-summary` to allow both branch routers to dynamically exchange subnet maps.
* **Security:** Hardened the management plane using **MD5-encrypted** `enable secret` passwords to protect administrative access.

---

## 🗺️ Topology Diagram
![Network Topology](topology.png)

---

## 🚀 Key Commands Used

### 1. DHCP Pool Configuration (Local Automation)
```bash
ip dhcp pool OFFICE_LAN
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
interface Serial0/3/0
 ip address 10.0.0.1 255.255.255.252
 clock rate 128000
 no shutdown
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 192.168.1.0
enable secret [password]
line vty 0 4
 password [password]
 login
