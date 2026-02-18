# Lab: Investigate Static Routes (IPv4 & IPv6)

##  Project Overview
This lab demonstrates the configuration and verification of various Cisco static route types, including recursive, fully specified, and floating static routes. The topology ensures high availability between three sites using redundant serial links and Ethernet connections.



##  Topology & Addressing
The network consists of three Cisco routers (R1, R2, R3). Each router uses a Loopback interface to simulate a local area network (LAN).

| Device | Interface | IPv4 Address | IPv6 Address |
| :--- | :--- | :--- | :--- |
| **R1** | Loopback0 | 192.168.1.1/27 | 2001:DB8:ACAD:1000::1/64 |
| **R2** | Loopback0 | 192.168.2.1/27 | 2001:DB8:ACAD:2000::1/64 |
| **R3** | Loopback0 | 192.168.3.1/27 | 2001:DB8:ACAD:3000::1/64 |

##  Configuration Highlights

### 1. Floating Static Routes (Redundancy)
To provide failover, R1 and R3 are connected by two serial links. The primary link has a default Administrative Distance (AD), while the backup link uses a higher AD to "float" above the primary.
- **IPv4 Backup:** AD 7
- **IPv6 Backup:** AD 17

### 2. Fully Specified Routes
Used for IPv6 connectivity where a Link-Local address is the next hop, requiring the explicit definition of the exit interface.



##  Verification Results

### End-to-End Connectivity
Verified via ICMP pings from R1 Loopback to R3 Loopback:
```bash
R1# ping 192.168.3.1 source loopback0
!!!!!
Success rate is 100 percent (5/5)
