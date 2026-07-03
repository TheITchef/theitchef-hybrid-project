# homelab-svi-config
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

================================================================================
## 1. Purpose
================================================================================
This document defines the SVI (Switched Virtual Interface) configuration for the
WS‑C3850 core switch.  
SVIs provide Layer 3 gateways for all VLANs in the homelab.

================================================================================
## 2. SVI Addressing Summary
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

================================================================================
## 3. SVI Configuration (WS‑C3850)
================================================================================

### VLAN 99 — PAWs (Tier‑0 Admin)
```cisco
interface Vlan99
 description PAWs (Tier-0 Admin)
 ip address 192.168.99.1 255.255.255.0
 ip helper-address 192.168.10.10
 no shutdown

VLAN 100 — Management / OOB
cisco

interface Vlan100
 description Management / OOB
 ip address 192.168.100.1 255.255.255.0
 ip helper-address 192.168.10.10
 ip access-group OOB-PROTECT in
 no shutdown

VLAN 10 — Identity Services
cisco

interface Vlan10
 description Identity Services (AD DS, PKI, ADFS, WAP)
 ip address 192.168.10.1 255.255.255.0
 ip access-group IDENTITY-PROTECT in
 no shutdown

VLAN 20 — ESXi Hosts
cisco

interface Vlan20
 description ESXi Hosts (mgmt + vMotion)
 ip address 192.168.20.1 255.255.255.0
 ip helper-address 192.168.10.10
 ip access-group ESXI-PROTECT in
 no shutdown

VLAN 30 — VM Network
cisco

interface Vlan30
 description VM Network (MS01 workloads)
 ip address 192.168.30.1 255.255.255.0
 ip helper-address 192.168.10.10
 no shutdown

VLAN 90 — WAN Edge / Router Inside
cisco

interface Vlan90
 description WAN Edge / Router Inside
 ip address 192.168.90.1 255.255.255.0
 ip helper-address 192.168.10.10
 ip access-group ROUTER-PROTECT in
 no shutdown

================================================================================
4. Global Routing Configuration

================================================================================
cisco

ip routing

Default Route → Cisco 891F
cisco

ip route 0.0.0.0 0.0.0.0 192.168.90.254

================================================================================
5. Notes

================================================================================

    All SVIs are hosted on the WS‑3850; no SVIs exist on the 3560CG.

    DHCP relay points to DC01 (192.168.10.10).

    ACLs applied only on Identity, ESXi, OOB, and Router VLANs.

    PAW VLAN (99) intentionally has no ACL inbound.

    Router inside interface resides in VLAN 90.

================================================================================
END OF DOCUMENT
================================================================================