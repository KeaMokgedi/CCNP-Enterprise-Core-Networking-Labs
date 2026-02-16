# Cisco Lab: Advanced STP Modifications and Protection Mechanisms

##  Project Overview
This lab focuses on "bending" the Spanning Tree Protocol (STP) to meet specific network design requirements. Beyond basic loop prevention, this project demonstrates **Multi-VLAN Load Balancing**, **Path Manipulation** using costs and priorities, and **Topology Protection** to ensure network stability against rogue devices.

##  Network Topology
The network consists of three switches in a redundant triangle:
* **D1 & D2**: Cisco 3650 Multilayer Switches (Core/Distribution)
* **A1**: Cisco 2960 Switch (Access)


##  Implementation Phases

### **1. Multi-VLAN Load Balancing**
I configured the network so that traffic for different VLANs takes different paths, utilizing all available bandwidth.
* **VLAN 1**: D1 is the Primary Root; D2 is the Secondary Root.
* **VLAN 2**: D2 is the Primary Root; D1 is the Secondary Root.

### **2. Path Manipulation**
To control exactly which cables carry traffic, I adjusted the following:
* **Port Cost**: Reduced A1's `Fa0/2` cost to **12** to force it as the Root Port for VLAN 1.
* **Port Priority**: Modified D2's `Gi1/0/6` priority to **64** to force A1 to prefer `Fa0/4` for VLAN 2 traffic.

### **3. Topology Protection**
To secure the Layer 2 domain, the following mechanisms were implemented:
* **PortFast (Edge Ports)**: Enabled on `Fa0/23` to allow end-devices immediate network access.
* **Root Guard**: Configured on D2 ports to prevent unauthorized switches from becoming the Root Bridge.
* **BPDU Guard**: (Optional Step) Prevents loops on Edge Ports by disabling them if a BPDU is detected.

##  Verification Evidence

### **VLAN Load Balancing (D1 Output)**
```text
VLAN0001: This bridge is the root (Priority 24577)
VLAN0002: Root Port is Gi1/0/1 (Priority 28674)
