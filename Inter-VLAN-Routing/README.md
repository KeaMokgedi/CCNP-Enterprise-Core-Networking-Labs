# Packet Tracer - Configure Basic Router Settings (Physical Mode)

## Project Overview
This lab involves setting up a Cisco 4321 ISR in **Physical Mode** within Packet Tracer. The objective is to perform a secure initial configuration, establish IPv4 and IPv6 connectivity, and harden the device for remote management via SSH.

## Topology
The network consists of a Cisco 4321 Router (R1) connected directly to a Server and a PC. A Loopback interface is used for management simulation.

| Device | Interface | IP Address | Subnet/Prefix | Default Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/0/0 | 192.168.0.1 | /24 | N/A |
| **R1** | G0/0/1 | 192.168.1.1 | /24 | N/A |
| **R1** | Loopback0 | 10.0.0.1 | /24 | N/A |
| **PC-A** | NIC | 192.168.1.10 | /24 | 192.168.1.1 |
| **Server** | NIC | 192.168.0.10 | /24 | 192.168.0.1 |

## Key Configurations Implemented

### 1. Device Security
* **Password Encryption:** Enabled via `service password-encryption`.
* **Password Complexity:** Enforced a minimum length of 12 characters.
* **Brute Force Protection:** Configured `login block-for 120 attempts 3 within 60` to prevent rapid login attempts.
* **Banner:** Implemented a MOTD to warn against unauthorized access.

### 2. Remote Management (SSH)
* **Domain Name:** Set to `ccna-lab.com`.
* **Crypto Keys:** Generated 1024-bit RSA keys to enable the SSH daemon.
* **Transport Security:** VTY lines configured for `transport input ssh` only, disabling insecure Telnet.
* **Local Auth:** Created a privileged user `SSHadmin` for local database login.

### 3. IP Connectivity
* **Dual-Stack:** Configured both IPv4 and IPv6 on all active interfaces.
* **IPv6 Routing:** Enabled using `ipv6 unicast-routing`.
* **Interface Management:** Descriptions added to all interfaces and brought to an "Up/Up" state.

## Verification Commands
The following commands were used to verify the configuration and hardware status:

* `show ip interface brief`: To verify IPv4 interface status.
* `show ipv6 interface brief`: To verify IPv6 and Link-Local addresses.
* `show version`: To identify IOS image name and memory (NVRAM/Flash) capacity.
* `show ip route`: To confirm directly connected networks.

## Lab Questions & Reflections
* **Telnet Security:** Telnet is a risk because it transmits data in plaintext, whereas SSH encrypts the session.
* **Config Register (0x2142):** Setting the register to 0x2142 causes the router to ignore the startup-config on boot, typically used for password recovery.
* **Status [up/up]:** Indicates that the physical layer (Layer 1) and data link layer protocol (Layer 2) are both functional.

---
*Completed as part of the Cisco Networking Academy CCNA curriculum.*
