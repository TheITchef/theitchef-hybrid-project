# homelab-routing-plan
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

================================================================================
## 1. Purpose
================================================================================
This document defines the Layer 3 routing architecture for the homelab.  
It establishes:
- SVI interfaces on the WS‑3850 (core L3 switch)
- Inter‑VLAN routing behavior
- Router (Cisco 891F) inside interface routing
- DHCP relay paths
- DNS reachability
- PAW full-access routing model

ACLs are intentionally excluded due to prior issues with the 891F.  
ACLs will be added in a separate document after validation.

================================================================================
## 2. Routing Model Overview
================================================================================
Routing is performed exclusively on the WS‑3850.  
The WS‑3850 hosts all SVI interfaces and acts as the default gateway for all VLANs.

The Cisco 891F provides WAN connectivity only.  
Its inside interface resides in VLAN 90.

PAWs (VLAN 99) have full routed access to all VLANs via the WS‑3850.

================================================================================
## 3. SVI Definitions (WS‑3850)
================================================================================

| VLAN ID | Name            | Subnet           | Gateway IP        |
|--------|------------------|------------------|-------------------|
| 1      | Native           | (unused)         | n/a               |
| 99     | PAWs             | 192.168.99.0/24  | 192.168.99.1      |
| 100    | Mgmt/OOB         | 192.168.100.0/24 | 192.168.100.1     |
| 10     | Identity         | 192.168.10.0/24  | 192.168.10.1      |
| 20     | ESXi Hosts       | 192.168.20.0/24  | 192.168.20.1      |
| 30     | VM Network       | 192.168.30.0/24  | 192.168.30.1      |
| 90     | WAN Edge         | 192.168.90.0/24  | 192.168.90.1      |

SVIs are configured on the WS‑3850 as follows:

interface Vlan99
ip address 192.168.99.1 255.255.255.0

interface Vlan100
ip address 192.168.100.1 255.255.255.0

interface Vlan10
ip address 192.168.10.1 255.255.255.0

interface Vlan20
ip address 192.168.20.1 255.255.255.0

interface Vlan30
ip address 192.168.30.1 255.255.255.0

interface Vlan90
ip address 192.168.90.1 255.255.255.0
Code


================================================================================
## 4. Inter‑VLAN Routing Behavior
================================================================================
The WS‑3850 performs all routing between VLANs.

### Default behavior:
- All VLANs can reach each other (no ACLs applied yet).
- PAWs (VLAN 99) can reach all VLANs.
- Identity services (VLAN 10) can reach ESXi (20), VM network (30), and OOB (100).
- ESXi hosts (VLAN 20) can reach identity (10) and VM network (30).
- VM workloads (VLAN 30) can reach identity (10) and ESXi (20).
- OOB (VLAN 100) can reach all VLANs for management purposes.

### Router reachability:
- VLAN 99 → VLAN 90 → Router inside interface
- VLAN 10 → VLAN 90 → Router inside interface
- VLAN 30 → VLAN 90 → Router inside interface

Routing is deterministic and broadcast-free.

================================================================================
## 5. Router (Cisco 891F) Routing
================================================================================
The Cisco 891F has:
- WAN interface (Gi0/0) → ISP
- Inside interface (Gi0/1) → VLAN 90 trunk

Inside IP:

interface GigabitEthernet0/1
description LAN Inside
encapsulation dot1Q 90
ip address 192.168.90.254 255.255.255.0
Code


### Default route (WS‑3850 → 891F)

ip route 0.0.0.0 0.0.0.0 192.168.90.254
Code


### LAN route (891F → WS‑3850)

ip route 192.168.0.0 255.255.0.0 192.168.90.1
Code


This ensures:
- All LAN VLANs route through the WS‑3850
- All WAN-bound traffic routes through the 891F

================================================================================
## 6. DHCP Relay
================================================================================
DHCP server: DC01 (VLAN 10)

DHCP relay is configured on the WS‑3850 SVIs:

interface Vlan99
ip helper-address 192.168.10.10

interface Vlan100
ip helper-address 192.168.10.10

interface Vlan20
ip helper-address 192.168.10.10

interface Vlan30
ip helper-address 192.168.10.10

interface Vlan90
ip helper-address 192.168.10.10
Code


Identity VLAN (10) does not require relay.

================================================================================
## 7. DNS Reachability
================================================================================
DNS servers:  
- DC01 → 192.168.10.10  
- Secondary DC (VM) → 192.168.10.11

All VLANs must be able to reach DNS on VLAN 10.

Routing ensures:
- PAWs (99) → DNS (10)
- ESXi (20) → DNS (10)
- VM workloads (30) → DNS (10)
- OOB (100) → DNS (10)
- Router (90) → DNS (10)

================================================================================
## 8. PAW Routing Model
================================================================================
PAWs (VLAN 99) have full routed access to all VLANs.

Path to router:

PAW → VLAN 99 → SVI 99 → WS‑3850 routing → SVI 90 → Router
Code


Path to identity:

PAW → VLAN 99 → SVI 99 → WS‑3850 routing → SVI 10 → DC01
Code


Path to ESXi:

PAW → VLAN 99 → SVI 99 → WS‑3850 routing → SVI 20 → ESXi01/02
Code


Path to VM workloads:

PAW → VLAN 99 → SVI 99 → WS‑3850 routing → SVI 30 → MS01
Code


No ACLs applied yet.

================================================================================
## 9. Future ACL Plan (Separate Document)
================================================================================
ACLs will be added in:
`network/homelab-routing-acls.md`

They will:
- Protect identity VLAN
- Protect PKI
- Restrict ESXi mgmt
- Restrict OOB
- Maintain PAW full access
- Protect router inside interface

ACLs will be validated on the WS‑3850 before touching the 891F.

================================================================================
END OF DOCUMENT
================================================================================