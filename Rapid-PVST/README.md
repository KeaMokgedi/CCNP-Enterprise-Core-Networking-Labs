# Spanning Tree Traffic Engineering: Path Manipulation & Load Balancing

## 1. Project Overview
This lab demonstrates the implementation of a redundant, load-balanced switching topology using **Rapid Per-VLAN Spanning Tree (Rapid-PVST)**. The goal was to engineer traffic paths so that redundant physical links are utilized effectively rather than remaining idle in a blocking state.

Originally designed for **Multiple Spanning Tree (MST)**, this project highlights the ability to pivot protocols when hardware or simulator constraints (Packet Tracer) arise, while still achieving the desired architectural outcomes.

## 2. Topology Diagram
The network is built in a triangular redundancy pattern:
* **Distribution Layer:** Two Cisco 3560 Multilayer Switches (D1, D2).
* **Access Layer:** One Cisco 3560 Switch (A1).
* **Links:** Dual-homed redundant FastEthernet and GigabitEthernet connections.



## 3. Configuration Objectives
1. **Redundancy:** Ensure no physical loops exist while maintaining sub-second convergence.
2. **Root Bridge Alignment:** Distribute the "Root" roles so that different switches manage different VLANs.
3. **Traffic Engineering (Cost):** Manually influence path selection for VLAN 1.
4. **Traffic Engineering (Priority):** Manually influence path selection for VLAN 2.

## 4. Key Configurations

### A. Root Bridge Roles
By setting D1 as the primary for VLAN 1 and D2 for VLAN 2, we ensure that the "center" of the network depends on which VLAN is being used.

```ios
! On D1
spanning-tree vlan 1 root primary
spanning-tree vlan 2 root secondary

! On D2
spanning-tree vlan 2 root primary
spanning-tree vlan 1 root secondary
