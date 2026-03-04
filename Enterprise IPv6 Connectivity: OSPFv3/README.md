<img width="736" height="509" alt="Screenshot 2026-03-04 233658" src="https://github.com/user-attachments/assets/7bdc83f2-eba4-46eb-a896-18e2d274598c" />


# Multiarea OSPFv3 Implementation & Route Summarization

##  Project Overview
This project demonstrates the design and deployment of a scalable **IPv6 routing architecture** using **Multiarea OSPFv3**. The topology consists of a core backbone (Area 0) and two peripheral areas (Area 1 and Area 2), utilizing Cisco ISR 4321 routers and Layer 3 switches.

The implementation focuses on **Traditional OSPFv3 configuration** (interface-based), addressing common syntax constraints in Packet Tracer environments while achieving full enterprise-grade connectivity.

##  Topology Architecture
The network is divided into three logical OSPF areas:
* **Area 0 (Backbone):** Connects R1, R2, and R3.
* **Area 1:** Contains R1 and the D1 Multilayer Switch.
* **Area 2:** Contains R3 and the D2 Multilayer Switch.



##  Key Technical Features
* **Traditional OSPFv3 Configuration:** Enabled OSPFv3 directly on physical and loopback interfaces to bypass Address-Family limitations.
* **Inter-Area Route Summarization:** Configured ABRs (R1 and R3) to summarize `/64` subnets into `/52` prefixes to optimize the global routing table.
* **Passive Interfaces:** Hardened the LAN segments on D1 and D2 by suppressing OSPF Hello packets while still advertising the prefixes.
* **IPv4/IPv6 Dual-Stack (D2):** Demonstrated routing capability for both protocols on the Area 2 gateway.

##  Configuration Snippets

### ABR Summarization (R3)
```bash
ipv6 router ospf 123
 router-id 3.3.3.1
 area 2 range 2001:DB8:ACAD:2000::/52
