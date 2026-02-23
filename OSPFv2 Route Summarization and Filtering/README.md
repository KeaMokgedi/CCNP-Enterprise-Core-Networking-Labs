# OSPFv2 Route Summarization & Multi-Area Filtering Lab

##  Project Overview
This project demonstrates advanced OSPFv2 configuration within a multi-area hierarchy. The focus is on optimizing the **Link State Database (LSDB)** and the **Routing Table** through manual route summarization and LSA Type-3 filtering on Area Border Routers (ABRs).



##  Topology Architecture
The network is segmented into three distinct OSPF areas:
* **Area 0 (Backbone):** Connects R1, R2, and R3. R2 serves as the core backbone router.
* **Area 1 (Stub):** Managed by **D1** (L3 Switch) and **R1** (ABR).
* **Area 2 (Stub):** Managed by **D2** (L3 Switch) and **R3** (ABR). Supports high-density loopback networks.

##  Addressing Table
| Device | Interface | IP Address | OSPF Area |
| :--- | :--- | :--- | :--- |
| **R1** | G0/0/0 | 172.16.0.2/30 | Area 0 |
| **R1** | G0/0/1 | 10.10.0.1/30 | Area 1 |
| **R2** | G0/0/0 | 172.16.0.1/30 | Area 0 |
| **R2** | G0/0/1 | 172.16.1.1/30 | Area 0 |
| **R3** | G0/0/0 | 172.16.1.2/30 | Area 0 |
| **R3** | G0/0/1 | 10.10.4.1/30 | Area 2 |
| **D1** | G1/0/11 | 10.10.0.2/30 | Area 1 |
| **D2** | G1/0/11 | 10.10.4.2/30 | Area 2 |

##  Advanced Configurations

### 1. Inter-Area Route Summarization
To minimize the routing table size on the backbone (R2), binary calculation was performed to create summary ranges on the ABRs.

**On R1 (Summarizing Area 1):**
```bash
router ospf 123
 area 1 range 10.10.0.0 255.255.252.0
