# homelab-architecture-overview
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Upplands Väsby, Stockholm County, Sweden

================================================================================
## 1. Executive Summary
================================================================================
This document provides a high-level overview of the hybrid homelab architecture.
It defines the logical layers, physical topology, trust boundaries, and management
plane. It serves as the master reference for all future design tasks including
VLAN planning, addressing, identity services, PKI, and virtualization.

================================================================================
## 2. Logical Architecture Overview
================================================================================

### 2.1 Compute Layer
- DC01 — Active Directory Domain Services  / DHCP / DNS
- ESXi01 — ESXI Host (PROD/STAGING VMs)
- ESXi02 — Available , Role TBD (PROXMOX candidate)  
- MS01 — Microsoft Infra via Hyper V VMs

### 2.2 Network Layer
- Cisco WS-C3850-48P — Core switching / InterVLAN routing  
- Cisco WS-C3560CG-8PC-S — OOB / Managememt switching  
- Cisco C891F-K9 — Only WAN edge / No VLAN routing / TBD L3 routing

### 2.3 Identity Layer
- Active Directory Domain Services  
- Two-tier PKI  
- ADFS + WAP  
- Azure AD Connect (hybrid identity)

### 2.4 Security Layer
- Trust boundaries (LAN, WAN, OOB)  
- Authentication flows  
- Certificate services  
- Federation boundaries

### 2.5 Management Layer
- iDRAC / iLO  
- OOB switch  
- PAWs (PN52, T470s)  
- ESXi management (vmk0)

================================================================================
## 3. Physical Topology Overview
================================================================================

### 3.1 Rack-Level View (High-Level)
- Core switch (3850) as central aggregation  
- OOB switch (3560CG) for management plane  
- Router (891F) providing WAN uplink  
- Servers connected to core and OOB  
- PAWs accessing OOB + LAN

### 3.2 High-Level Diagram (ASCII)

+---------------------------+
|        WAN / ISP         |
+-------------+-------------+
|
[ Cisco 891F ]
|
+-------------+-------------+
|         Core Switch       |
|      Cisco WS-C3850       |
+-------------+-------------+
|
-------------------------------------------------
|                   |                         |
[DC01]             [ESXi01]                  [ESXi02]
|                   |                         |
-------------------------------------------------
|
[ MS01 Server ]
|
+-------------+-------------+
|         OOB Switch        |
|   Cisco WS-C3560CG-8PC-S  |
+-------------+-------------+
|
[ PAWs / Mgmt ]
Code


================================================================================
## 4. Trust Boundaries
================================================================================

### 4.1 Internal LAN
- Core switching  
- Servers  
- ESXi hosts  
- MS01 workloads  
- AD DS, PKI, ADFS

### 4.2 OOB Management Network
- iDRAC / iLO  
- ESXi vmk0  
- PAWs  
- OOB switch

### 4.3 WAN Boundary
- Router WAN interface  
- ISP handoff  
- Public-facing services (if any)

================================================================================
## 5. Management Plane Overview
================================================================================

### 5.1 Access Paths
- PAWs → OOB switch → iDRAC/iLO  
- PAWs → LAN → ESXi management  
- PAWs → LAN → DC01/MS01

### 5.2 Management Interfaces
- iDRAC8 Express / No dedicated Port  (DC01)  
- iDRAC7 Enterprise / Dedicated LAN port (ESXi01, ESXi02)  
- iLO4 Advanced / Dedicated LAN port (MS01)  
- ESXi vmk0  
- Switch mgmt SVI  
- Router mgmt

### 5.3 Out-of-Band Strategy
- Dedicated OOB switch  
- Segregated mgmt VLAN  
- PAW-only access  
- No production traffic

================================================================================
## 6. Dependencies & Future Work
================================================================================

### 6.1 Required Next Documents
- homelab-vlan-plan  
- homelab-addressing-plan  
- homelab-oob-design  
- homelab-pki-architecture  
- homelab-ad-architecture  
- homelab-esxi-networking-overview

### 6.2 Required Configurations
- VLAN creation  
- IP addressing  
- Routing  
- ESXi vSwitch design  
- PKI deployment  
- ADFS/WAP configuration  
- Azure AD Connect setup

================================================================================
## 7. Notes
================================================================================
- This document is intentionally high-level.  
- Detailed configurations will be defined in downstream documents.  
- This overview is the baseline for all future homelab design tasks.

================================================================================
END OF DOCUMENT
================================================================================