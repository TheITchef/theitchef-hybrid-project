md

# homelab-vlan-plan
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

================================================================================
## 1. Overview
================================================================================
This document defines the VLAN segmentation and trunking strategy for the hybrid
homelab. It establishes Layer 2 boundaries, management isolation, uplink design,
and switch-to-switch relationships required for stable network operation.

The VLAN plan supports:
- Identity services (AD DS, PKI, ADFS, Azure AD Connect)
- ESXi virtualization
- VM workloads
- Privileged Access Workstations (PAWs)
- Out-of-band (OOB) management
- WAN edge routing

================================================================================
## 2. VLAN Definitions
================================================================================
| VLAN ID | Name                   | Purpose                                      |
|--------|-------------------------|----------------------------------------------|
| 1      | Native                 | Native VLAN (kept clean)                     |
| 99     | PAWs (Tier‑0 Admin)    | PN52, T470s — full routed access to all VLANs |
| 100    | Management / OOB       | Switch mgmt, iDRAC/iLO, ESXi vmk0            |
| 10     | Identity Services      | AD DS, PKI, ADFS, WAP, Azure AD Connect      |
| 20     | ESXi Hosts             | ESXi mgmt, vMotion, hypervisor control       |
| 30     | VM Network             | MS01 workloads, general VMs                  |
| 90     | WAN Edge               | Router internal interface                     |

================================================================================
## 3. VLAN Roles
================================================================================
- **Native (1):** Kept clean, no production workloads.
- **PAWs (99):** Full routed access to all VLANs; Tier‑0 administrative zone.
- **Management/OOB (100):** Switch mgmt, iDRAC/iLO, ESXi vmk0.
- **Identity (10):** Domain controllers, PKI, ADFS, WAP, Azure AD Connect.
- **ESXi Hosts (20):** ESXi mgmt, vMotion, hypervisor control traffic.
- **VM Network (30):** General VM workloads (MS01, application servers).
- **WAN Edge (90):** Router internal interface; boundary between LAN/WAN.

================================================================================
## 4. Trunking Strategy
================================================================================

### 4.1 WS‑3850 ↔ C3560CG (OOB Switch)
- Mode: trunk  
- Native VLAN: 1  
- Allowed VLANs: 1,10,20,30,90,99,100  

interface Gig1/0/x
switchport mode trunk
switchport trunk native vlan 1
switchport trunk allowed vlan 1,10,20,30,90,99,100
spanning-tree portfast trunk
Code


### 4.2 WS‑3850 ↔ ESXi01
- Mode: trunk  
- Native VLAN: 1  
- Allowed VLANs: 1,10,20,30,99,100  

interface TenGig1/1/x
switchport mode trunk
switchport trunk native vlan 1
switchport trunk allowed vlan 1,10,20,30,99,100
spanning-tree portfast trunk
Code


### 4.3 WS‑3850 ↔ ESXi02
Same as ESXi01.

### 4.4 WS‑3850 ↔ Hyper‑V Host (DL360 G8)
- Mode: trunk  
- Native VLAN: 1  
- Allowed VLANs: 1,10,20,30,99,100  

interface Gig1/0/x
switchport mode trunk
switchport trunk native vlan 1
switchport trunk allowed vlan 1,10,20,30,99,100
spanning-tree portfast trunk
Code


### 4.5 WS‑3850 ↔ Router (Cisco 891F)
- Mode: trunk  
- Native VLAN: 1  
- Allowed VLANs: 1,90  

interface Gig1/0/x
switchport mode trunk
switchport trunk native vlan 1
switchport trunk allowed vlan 1,90
spanning-tree portfast trunk
Code


================================================================================
## 5. Access Port Strategy
================================================================================

### PAWs (PN52, T470s)

switchport mode access
switchport access vlan 99
spanning-tree portfast
Code


### OOB Devices (iDRAC/iLO, ESXi mgmt if access)

switchport mode access
switchport access vlan 100
spanning-tree portfast
Code


### Identity Services (DC01, ADFS, PKI)

switchport mode access
switchport access vlan 10
spanning-tree portfast
Code


### VM Workloads (MS01)

switchport mode access
switchport access vlan 30
spanning-tree portfast
Code


================================================================================
## 6. High-Level VLAN Flow Diagram
================================================================================

+---------------------------+
|        WAN / ISP         |
+-------------+-------------+
|
[ Router ]
VLAN 90
|
+-------------+-------------+
|         Core Switch       |
|          WS-C3850         |
+-------------+-------------+
-------------------------------------------------
|                   |                         |
VLAN 10             VLAN 20                   VLAN 30
Identity Zone       ESXi Hosts Zone           VM Network Zone
|                   |                         |
[DC01]             [ESXi01]                  [MS01]
|
[ ESXi02 ]
|
+-------------+-------------+
|         OOB Switch        |
|     WS-C3560CG-8PC-S      |
+-------------+-------------+
|
VLAN 99 (PAWs)
Code


================================================================================
## 7. Dependencies
================================================================================
- homelab-addressing-plan  
- homelab-routing-plan  
- homelab-esxi-networking-overview  
- homelab-oob-design  
- homelab-pki-architecture  
- homelab-ad-architecture  

================================================================================
## 8. Notes
================================================================================
- PAWs (VLAN 99) have full routed access to all VLANs via WS‑3850 SVIs.
- Router is isolated in VLAN 90 to reduce broadcast exposure.
- Native VLAN 1 remains unused for production traffic.
- All trunks use VLAN 1 as native for consistency.
- VLAN numbering preserves lower tens for future expansion.

================================================================================
END OF DOCUMENT
================================================================================

If you want, I can now generate the routing ACL section, the addressing plan, or the device‑to‑VLAN mapping.