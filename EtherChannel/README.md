# Lab: Implement EtherChannel (PAgP, LACP, and Static)

## 1. Project Overview

This project documents the configuration and verification of Link Aggregation (EtherChannel) across a Cisco switched topology. The goal was to increase inter-switch bandwidth and provide redundancy while managing Spanning Tree Protocol (STP) behavior.

---

## 2. Topology & Resources

- **D1 (3650):** VTP Server & EtherChannel Endpoint (PAgP/LACP)  
- **D2 (3650):** VTP Transparent & EtherChannel Endpoint (LACP/Static)  
- **A1 (2960+):** VTP Client & EtherChannel Endpoint (PAgP/Static)

---

## 3. Configuration Highlights

### Disabling DTP (Dynamic Trunking Protocol)

To ensure security and manual control over trunks, DTP was disabled on all physical member ports.

**Commands used:**
```
switchport mode trunk
switchport nonegotiate
```

### EtherChannel Implementation

Three distinct channel-group modes were used to demonstrate protocol variety:

- **Static (Mode On):** Configured between D2 and A1.  
- **PAgP (Cisco Proprietary):** Configured between D1 and A1 using mode desirable.  
- **LACP (IEEE Standard):** Configured between D1 and D2 using mode active.

---

## 4. Verification & Status Outputs

The following outputs confirm all Port-channels achieved the (SU) state (Layer 2, In Use).

### Switch D1 Status
```
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
2      Po2(SU)           PAgP   Gig1/0/5(P) Gig1/0/6(P)
3      Po3(SU)           LACP   Gig1/0/1(P) Gig1/0/2(P) Gig1/0/3(P) Gig1/0/4(P)
```

### Switch A1 Status
```
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
1      Po1(SU)           -      Fa0/3(P) Fa0/4(P)
2      Po2(SU)           PAgP   Fa0/1(P) Fa0/2(P)
```

### Switch D2 Status
```
Group  Port-channel  Protocol    Ports
------+-------------+-----------+----------------------------------------------
1      Po1(SU)           -      Gig1/0/5(P) Gig1/0/6(P)
3      Po3(SU)           LACP   Gig1/0/1(P) Gig1/0/2(P) Gig1/0/3(P) Gig1/0/4(P)
```

---

## 5. Lessons Learned

- **Configuration Consistency:** Any mismatch in speed, duplex, or VLAN assignment results in a "Suspended" (s) or "Independent" (I) state.  

- **Logical Management:** All trunking and native VLAN configurations (VLAN 999) must be applied to the interface port-channel to ensure all member links stay synchronized.  

- **Hardware Limits:** Older IOS versions on the 2960+ may not support specific protocol keywords like `non-silent`.

---

**Course:** CCNP Enterprise - Advanced Routing and Switching  
**Lab Reference:** NetAcad - Implement EtherChannel
