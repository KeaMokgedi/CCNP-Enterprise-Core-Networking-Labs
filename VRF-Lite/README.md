# Multi-Customer Dual-Stack Network Infrastructure
A comprehensive implementation of a Service Provider hub-and-spoke topology, providing isolated Site-to-Site connectivity for multiple customers using legacy Serial links and modern 802.1Q sub-interfaces.

##  Project Overview
This lab demonstrates the configuration of a Service Provider router (**R1**) that manages two distinct customer environments. The project highlights the ability to provide traffic separation and routing in an environment where VRF (Virtual Routing and Forwarding) is not supported by the hardware license.

### Customer Architecture
* **Customer A:** Connectivity via Serial (`S0/1/0`) and Physical Gigabit links.
* **Customer B:** Connectivity via a single trunked link utilizing **Router-on-a-Stick** logic with VLANs 5 and 8.

##  Technical Implementation
### 1. Layer 2 Isolation
Since VRF was unavailable, isolation for Customer B was achieved at Layer 2 using **Switch A1**:
- **VLAN 5:** Allocated for Customer B - Site 1.
- **VLAN 8:** Allocated for Customer B - Site 2.
- **Trunking:** 802.1Q trunk configured on `Fa0/11` to carry tagged traffic to the Provider Hub.

### 2. Provider Hub (R1) Configuration
The core router uses sub-interfaces to provide gateways for the tagged traffic:
```text
interface GigabitEthernet0/0/1.5
 encapsulation dot1Q 5
 ip address 10.1.20.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:2012::1/64

interface GigabitEthernet0/0/1.8
 encapsulation dot1Q 8
 ip address 10.1.30.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:2013::1/64
