# Multi-Area Network Design & Implementation

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Cisco](https://img.shields.io/badge/Cisco-Packet_Tracer-blue)
![Routing](https://img.shields.io/badge/Routing-OSPF%20%7C%20EIGRP%20%7C%20RIP-lightgrey)
![Addressing](https://img.shields.io/badge/Addressing-VLSM%20%7C%20IPv4-orange)

## 📌 Project Overview
This project, developed in Cisco Packet Tracer (`i242095.pkt`), demonstrates a comprehensive enterprise-level network design. It features multiple routing domains interconnected via route redistribution, centralized services, and security measures applied across 11 distinct networks supporting between 27K and 117K hosts.

---

## 📸 Network Topology
<!-- ⚠️ ACTION REQUIRED: Add a screenshot of your overall Packet Tracer topology here -->
![Network Topology Screenshot](docs/images/topology.png)
*(Caption: Full network topology showing all interconnected areas and devices)*

---

## 🚀 Key Features

| Feature | Description |
| :--- | :--- |
| **VLSM Subnetting** | Efficient IP allocation for 11 networks with varying host requirements (27K-117K hosts). |
| **Multi-Protocol Routing** | **OSPF Area 1**, **EIGRP AS 5**, **OSPF Area 2**, and **RIPv2** running simultaneously. |
| **Route Redistribution** | Mutual redistribution at 3 border routers enabling full end-to-end connectivity across all routing domains. |
| **Centralized DHCP** | Single DHCP server (`Server1`) serving all 11 networks dynamically via DHCP relay agents (IP Helper addresses). |
| **Email Services** | SMTP/POP3 mail server with DNS configured on `Server0` for intra-network email communication. |
| **NAT (Network Address Translation)** | Static NAT configured on `Router17` to translate private addresses to public addresses for external access. |
| **Security (ACLs)** | Extended Access Control Lists (ACLs) restricting specific host and subnet access to the web server. |
| **Redundant Paths** | Multiple parallel WAN links providing high network resilience and fault tolerance. |

---

## 🏗️ Routing Architecture

The network is divided into four distinct routing domains to optimize traffic and simulate a large-scale ISP/Enterprise connection model.

| Domain | Protocol | Routers Included | Networks Served |
| :--- | :--- | :--- | :--- |
| **OSPF Area 1** | OSPF Process 1, Area 1 | Router4, Router1, Router0, Router2 | Networks A, B, C |
| **EIGRP 5** | EIGRP AS 5 | Router2, Router3, Router5, Router6, Router7, Router9, Router8, Router10 | Networks D, E, F |
| **OSPF Area 2** | OSPF Process 1, Area 2 | Router10, Router11, Router12, Router13, Router18 | Networks G, H, I |
| **RIPv2** | RIP Version 2 | Router18, Router14, Router15, Router16, Router17 | Networks J, K |

<!-- ⚠️ ACTION REQUIRED: Add a screenshot highlighting the routing domains (e.g., color-coded sections in Packet Tracer) -->
![Routing Domains](docs/images/routing_domains.png)

---

## 📊 VLSM Subnetting Table

The IP addressing scheme utilizes Variable Length Subnet Masking (VLSM) to minimize IP waste across 11 major networks.

<!-- ⚠️ ACTION REQUIRED: Fill in your specific Network IPs, Subnet Masks, and Usable Ranges below based on your calculations -->
| Network | Required Hosts | Allocated Subnet (CIDR) | Subnet Mask | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Network A** | 66,778 | 10.0.0.0 /15 | 255.254.0.0 | 10.0.0.1 |
| **Network B** | 99,001 | 10.2.0.0 /15 | 255.254.0.0 | 10.2.0.1 |
| **Network C** | 22,345 | 10.14.0.0 /16 | 255.255.128.0 | 10.14.0.1 |
| **Network D** | 55,667 | 10.12.0.0 /16 | 255.255.0.0 | 10.12.0.1 |
| **Network E** | 88,990 | 10.13.0.0 /15 | 255.254.0.0 | 10.13.0.1 |
| **Network F** | 11,234 | 10.16.0.0 /18 | 255.255.192.0 | 10.16.0.1 |
| **Network G** | 44,556 | 10.11.0.0 /16 | 255.255.0.0 | 10.11.0.1 |
| **Network H** | 77,889 | 10.10.0.0 /15 | 255.254.0.0 | 10.10.0.1 |
| **Network I** | 99,002 | 10.8.0.0 /15 | 255.254.0.0 | 10.8.0.1 |
| **Network J** | 22,334 | 10.54.0.0 /17 | 255.255.128.0 | 10.54.0.1 |
| **Network K** | 55,667 | 10.1.0.0 /16 | 255.255.0.0 | 10.1.0.1 |

---

## 📟 Device Inventory

Based on the topology, the network consists of the following hardware:

*   **Routers (19):** Router0 through Router18. (Acting as Core, Border, and Edge routers).
*   **Switches (~11+):** Connecting end devices within Networks A through K.
*   **Servers (3+):**
    *   `Server0`: DNS & Email (SMTP/POP3)
    *   `Server1`: Centralized DHCP Server
    *   `Web Server`: Target for NAT and ACL testing.
*   **End Devices:** Various PCs and Laptops distributed across the 11 VLSM networks.

---

## ⚙️ Testing & Verification

To verify the functionality of this network, run the following tests in Packet Tracer:

### 1. End-To-End Connectivity (Ping)
Test ICMP communication from a PC in Network A (OSPF Area 1) to a PC in Network K (RIPv2).
<!-- ⚠️ ACTION REQUIRED: Add a screenshot of a successful ping across the network -->
![Successful Ping](docs/images/ping_test.png)

### 2. Route Redistribution Verification
Check the routing table on the border routers (e.g., Router2, Router10, Router18) to ensure external routes (`O E2`, `D EX`, `R`) are being injected.
```bash
Router# show ip route
```
<!-- ⚠️ ACTION REQUIRED: Add a screenshot of the 'show ip route' command from a border router -->
![Routing Table Screenshot](docs/images/routing_table.png)

### 3. DHCP Allocation
Ensure devices on edge networks successfully receive IP configurations from `Server1`.
<!-- ⚠️ ACTION REQUIRED: Add a screenshot of a PC successfully grabbing a DHCP IP -->
![DHCP Success](docs/images/dhcp_success.png)

### 4. ACL Restrictions
Attempt to ping/access the Web Server from a blocked IP or Subnet to verify the Extended ACL drops the packet.
<!-- ⚠️ ACTION REQUIRED: Add a screenshot showing "Destination Host Unreachable" or blocked traffic through simulation mode -->
![ACL Blocked](docs/images/acl_block.png)

---

## 🛠️ How to open the project

1. Download and install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer).
2. Clone or download this repository.
3. Open the `i242095.pkt` file in Cisco Packet Tracer.
4. Allow a few moments for the routing protocols (OSPF, EIGRP, RIP) to converge. Green indicators should appear on all active link interfaces.

---

## 👨‍💻 Authors

**Muhammad Zubair Tariq**
* **Roll Number:** 24i-2095
* **Program:** BS Cyber Security - 4th Semester
* **University:** FAST National University of Computer and Emerging Sciences
* **GitHub:** [@Zubair378](https://github.com/Zubair378)

---

