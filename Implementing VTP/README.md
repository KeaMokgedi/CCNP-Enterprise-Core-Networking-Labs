# Lab: Implementing VTP (VLAN Trunking Protocol)

##  Project Overview
This project demonstrates the implementation of **VTP Version 2** in a Cisco switched network. The lab focuses on centralized VLAN management, the role of configuration revision numbers, and the behavioral differences between VTP Server, Client, and Transparent modes.

> **Note:** While the initial lab scope included VTPv3, hardware limitations (IOS capable of VTP 1-2 only) required a pivot to a robust VTPv2 implementation.

---

##  Topology & Resources
* **D1 (VTP Server):** The authoritative source for VLAN configurations.
* **D2 (VTP Transparent):** Acts as a pass-through for VTP advertisements without updating its local database.
* **A1 (VTP Client):** Synchronizes its VLAN database based on updates from D1.
* **Domain Name:** `CCNPv8`
* **VTP Password:** `cisco123`

---

##  Configuration Guide

### 1. Basic Trunking
For VTP to communicate, all inter-switch links must be configured as 802.1Q trunks.
```ios
interface Range g1/0/1, g1/0/5-6
 switchport mode trunk
 switchport trunk encapsulation dot1q
 no shutdown
