
# Lab - Tune and Optimize EtherChannel Operations

This repository contains the configuration and verification steps for optimizing LACP-based EtherChannel operations on Cisco Catalyst 3650 switches (IOS XE).

## 1. Network Topology
* **Switches:** 2 x Cisco Catalyst 3650
* **Interconnections:** 4 x Gigabit Ethernet links (G1/0/1 through G1/0/4)
* **Protocol:** LACP (Link Aggregation Control Protocol)
* **Logical Interface:** Port-Channel 12

## 2. Configuration (Validated)

The following configuration was applied to both **D1** and **D2** to establish a Layer 2 Trunking EtherChannel.

```ios
! Configure physical member interfaces
interface range g1/0/1-4
 switchport mode trunk
 channel-group 12 mode active
 no shutdown
exit

! Configure the logical Port-Channel
interface port-channel 12
 switchport mode trunk
! Note: Manual min-links/max-bundle tuning omitted due to platform syntax variation
exit
