# Single-Area OSPFv2 Implementation on Cisco Catalyst & ISR

This project demonstrates a production-grade **Single-Area OSPFv2** deployment using a mix of Layer 3 Switches (Cisco 3650) and an ISR Router (Cisco 4321). 

##  Key Features
- **Multi-Vendor Logic:** Integration of L3 Switching (SVI-based routing) and traditional Routing.
- **Route Propagation:** Automated default-route injection from the Edge Router (R1) to the internal core.
- **Security & Optimization:** Implementation of `passive-interfaces` on user-facing segments to reduce CPU overhead and prevent neighbor spoofing.
- **Backbone Efficiency:** Adjusted `auto-cost reference-bandwidth` to 1000Mbps to support modern Gigabit links.

##  Topology Overview
- **Edge (R1):** Cisco 4321 - Acting as the ASBR (Autonomous System Boundary Router) for the simulated internet.
- **Distribution (D1 & D2):** Cisco 3650 L3 Switches - Handling inter-VLAN routing for 4 distinct departments.
- **Access (S1):** Cisco 2960 - Layer 2 backbone provider with a dedicated Management VLAN.

##  Addressing Table
| Device | Interface | IP Address | Purpose |
| :--- | :--- | :--- | :--- |
| R1 | G0/0/1 | 10.10.0.1/29 | Backbone DR |
| D1 | G1/0/5 | 10.10.0.2/29 | Backbone BDR |
| D2 | G1/0/5 | 10.10.0.3/29 | Backbone |
| S1 | VLAN 1 | 10.10.0.4/29 | Management |

##  Verification Commands
To verify the routing logic, use the following commands on the devices:
- `show ip ospf neighbor`: Confirm FULL adjacency.
- `show ip route ospf`: Verify OSPF-learned subnets and the `O*E2` default route.
- `show ip ospf interface`: View DR/BDR election status and hello timers.
