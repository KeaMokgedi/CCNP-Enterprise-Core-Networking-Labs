
# Cisco Lab: Observe STP Topology Changes and Implement RSTP

##  Project Overview
This project demonstrates the implementation and verification of **Spanning Tree Protocol (STP)** and **Rapid Spanning Tree Protocol (RSTP)** using Cisco 3650 and 2960 switches. The primary goal was to observe how Layer 2 loops are prevented and how RSTP significantly improves network convergence time compared to legacy STP.

##  Network Topology
The lab uses a triangular redundant topology to create potential loops, which are then managed by STP.

![Network Topology](./your_screenshot_name.png) 
*(Note: Ensure your screenshot file is in the same folder and named correctly here)*

### **Device Inventory**
* **D1**: Cisco 3650 (Root Bridge)
* **D2**: Cisco 3650 (Designated Switch)
* **A1**: Cisco 2960 (Access Switch)

##  Configuration Highlights
The switches were initially configured with standard PVST+ and later migrated to Rapid-PVST+ to optimize performance.

### **Key Commands**
```bash
# Set Spanning Tree Mode
spanning-tree mode rapid-pvst

# Verify Spanning Tree State
show spanning-tree vlan 1
show spanning-tree root
