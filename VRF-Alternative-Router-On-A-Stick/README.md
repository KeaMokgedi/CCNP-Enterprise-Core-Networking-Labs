## Multi-Customer Dual-Stack Network Infrastructure
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
 ```



## Troubleshooting & Evolution of Design

### The Initial Goal: VRF-Lite
The original objective was to implement **VRF-Lite (Virtual Routing and Forwarding)** to provide complete control-plane isolation for Customer A and Customer B. This would have allowed for overlapping IP addresses and independent routing tables on the provider hub (**R1**).

### The Roadblock: Hardware Constraints
During implementation, the following issues were encountered:
1. **Command Rejection:** The IOS version (15.4) on the specific hardware/image did not support the `ip vrf` or `vrf definition` commands.
2. **License Limitations:** Attempts to activate the `datak9` or `ipbase` features required for virtualization were unsuccessful due to the lab environment's licensing constraints.



### Steps Taken to Resolve
Before pivoting the design, several troubleshooting steps were performed:
* **Feature Set Verification:** Used `show version` and `show license` to identify available capabilities.
* **Syntax Investigation:** Checked for alternative syntax (e.g., legacy `ip vrf` vs. modern `vrf definition`).
* **Resource Assessment:** Evaluated if the router's memory and CPU could support multiple routing instances if the software was upgraded.

### The Pivot: "Router-on-a-Stick" Multi-Tenancy
Once it was confirmed that VRF was not an option, the architecture was redesigned to achieve **logical isolation** without virtual routing tables.

**Key Changes Made:**
1. **Sub-interface Mapping:** Created dedicated 802.1Q sub-interfaces on `G0/0/1` for Customer B, mapping them to specific VLANs (5 and 8) on the intermediate switch (**A1**).
2. **Unique Addressing Scheme:** Switched from a shared address space to unique, non-overlapping subnets to prevent routing table conflicts.
3. **Static Route Optimization:** Manually populated the Global Routing Table with specific static routes to ensure traffic from Site 1 could only reach Site 2 for the respective customer.
4. **IPv6 Enablement:** Manually enabled `ipv6 unicast-routing` across all devices to overcome the default behavior where IPv6 pings were failing despite having valid addresses.

### Lesson Learned
This lab highlights that **VRF is a luxury, not a necessity** for simple isolation. While VRF-Lite is the industry standard for scalability and overlapping address support, a well-engineered **Inter-VLAN Routing (IVR)** setup can achieve identical connectivity results on lower-tier hardware.
