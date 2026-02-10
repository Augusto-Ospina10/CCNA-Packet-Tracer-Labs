# Full-Stack Branch Connectivity Lab: DHCP, Serial WAN, & RIPv2

## 🎯 Project Objective
The goal of this project was to design and implement a complete network infrastructure for two geographically separated branch offices. This lab demonstrates mastery over local network services (DHCP), hardware modularity (Serial), and dynamic routing (RIPv2).

---

## 🏗️ Implementation Phases

### Phase 1: LAN Foundation & Local Services
* **Gateway Setup:** Configured GigabitEthernet 0/0 interfaces as the exit point for the 192.168.1.0/24 and 192.168.2.0/24 networks.
* **DHCP Configuration:** Configured routers as DHCP servers to automatically assign IP addresses and gateway info to all end-devices.

### Phase 2: WAN & Physical Interconnect
* **Hardware:** Installed **HWIC-2T** serial cards into the Cisco 2911 chassis.
* **Link Sync:** Applied a `clock rate 128000` on the **DCE** interface to synchronize bit-timing.
* **Addressing:** Utilized a point-to-point **/30** subnet (10.0.0.0/30) for efficiency.

### Phase 3: Dynamic Routing & Security
* **Routing:** Implemented **RIPv2** with `no auto-summary` to allow specific subnet advertisement.
* **Security:** Hardened the management plane using **MD5-encrypted** `enable secret` passwords.

---

## 🗺️ Topology Diagram
![Network Topology](topology.png)

---

## 🚀 Key Configurations (Combined CLI Snippet)

Below is the consolidated configuration applied to the routers to achieve full connectivity:

```bash
! --- SECTION 1: LAN & DHCP SERVICES ---
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown

ip dhcp pool BRANCH_OFFICE
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8

! --- SECTION 2: WAN INTERFACE (DCE) ---
interface Serial0/3/0
 ip address 10.0.0.1 255.255.255.252
 clock rate 128000
 no shutdown

! --- SECTION 3: DYNAMIC ROUTING (RIPv2) ---
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 192.168.1.0

! --- SECTION 4: DEVICE SECURITY ---
enable secret MySecurePassword123
🧪 Verification & Proof
Routing Table: Verified the presence of "R" routes via show ip route.

Connectivity: 100% success rate on ICMP pings between branch hosts.

Path Discovery: Confirmed the hop-by-hop path using tracert.

Author: Augusto Ospina

Project: CCNA Lab Portfolio
