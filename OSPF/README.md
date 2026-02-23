# Implement Single-Area OSPFv2 on Cisco Packet Tracer

This repository contains a completed Cisco Packet Tracer lab focused on implementing and optimizing **Single-Area OSPFv2** in a multiaccess Ethernet environment. 

The topology is unique as it utilizes **Layer 3 Switches** (Cisco 3650) alongside a traditional router to demonstrate advanced routing capabilities in a switched campus environment.

##  Topology Overview

The network consists of:
* **1x Cisco 4321 Router (R1):** Acting as the Gateway of Last Resort.
* **2x Cisco 3650 L3 Switches (D1, D2):** Providing routing services for internal subnets.
* **1x Cisco 2960 L2 Switch (S1):** Acting as the central multiaccess segment (VLAN 1).
* **4x End Devices (PCs):** Distributed across four different subnets.



##  Objectives
1. **Multiaccess Connectivity:** Configured a common `/29` subnet for the R1-D1-D2 backbone.
2. **OSPF Configuration:** Implemented OSPF using three distinct methods:
   - **R1:** Interface-specific configuration.
   - **D1:** Explicit IP address/Quad-zero mask.
   - **D2:** Subnet-specific wildcard masks.
3. **Route Propagation:** Configured R1 to originate a default static route to the simulated internet.
4. **Optimization:** - Adjusted `auto-cost reference-bandwidth` to 1000 Mbps for Gigabit Ethernet support.
   - Configured `passive-interfaces` on all user-facing LAN segments for security and overhead reduction.
   - Manually set `Router-IDs` (1.1.1.1, 2.2.2.2, 3.3.3.3) for predictable troubleshooting.

##  Addressing Table

| Device | Interface | IPv4 Address | Subnet Mask |
| :--- | :--- | :--- | :--- |
| R1 | G0/0/1 | 10.10.0.1 | 255.255.255.248 |
| D1 | G1/0/5 | 10.10.0.2 | 255.255.255.248 |
| D2 | G1/0/5 | 10.10.0.3 | 255.255.255.248 |
| PC1 | NIC | 10.10.8.10 | 255.255.255.0 |

##  How to Use
1. Download the `.pkt` file.
2. Open in **Cisco Packet Tracer (v8.0 or higher)**.
3. Verify OSPF adjacencies using:
   ```bash
   show ip ospf neighbor
   show ip route ospf
