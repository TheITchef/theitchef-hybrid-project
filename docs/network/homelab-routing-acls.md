# homelab-routing-acls
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

================================================================================
## 1. Purpose
================================================================================
This document defines the planned ACLs for routing and segmentation in the homelab,
with a focus on PAW (VLAN 99) full access and protection of identity, ESXi, OOB,
and router inside VLANs.

ACLs are designed for the WS‑3850 SVIs.  
ACLs on the Cisco 891F are intentionally avoided due to prior issues.

================================================================================
## 2. PAW Access Model
================================================================================
- PAWs (VLAN 99) must have full routed access to all VLANs.
- PAWs are treated as Tier‑0 admin endpoints.
- No ACL is applied inbound on VLAN 99.

================================================================================
## 3. ACL Definitions
================================================================================

### 3.1 PAW-FULL-ACCESS (Reference Only)
PAWs are allowed to reach any destination.  
No ACL is applied; this is conceptual only:

- Concept: `permit ip 192.168.99.0 0.0.0.255 any`

### 3.2 IDENTITY-PROTECT
Protects Identity VLAN (10) while allowing PAWs and DC traffic.

```cisco
ip access-list extended IDENTITY-PROTECT
 remark Permit PAWs to Identity
 permit ip 192.168.99.0 0.0.0.255 192.168.10.0 0.0.0.255
 remark Permit Identity to PAWs
 permit ip 192.168.10.0 0.0.0.255 192.168.99.0 0.0.0.255
 remark Deny all other VLANs to Identity
 deny   ip any 192.168.10.0 0.0.0.255
 remark Permit Identity to any (DCs must reach all)
 permit ip 192.168.10.0 0.0.0.255 any

3.3 ESXI-PROTECT

Protects ESXi mgmt VLAN (20) while allowing PAWs and Identity.
cisco

ip access-list extended ESXI-PROTECT
 remark Permit PAWs to ESXi
 permit ip 192.168.99.0 0.0.0.255 192.168.20.0 0.0.0.255
 remark Permit ESXi to PAWs
 permit ip 192.168.20.0 0.0.0.255 192.168.99.0 0.0.0.255
 remark Permit Identity to ESXi (DCs)
 permit ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
 remark Deny all other VLANs to ESXi
 deny   ip any 192.168.20.0 0.0.0.255
 remark Permit ESXi to any (for mgmt/updates)
 permit ip 192.168.20.0 0.0.0.255 any

3.4 OOB-PROTECT

Protects OOB VLAN (100) while allowing PAWs.
cisco

ip access-list extended OOB-PROTECT
 remark Permit PAWs to OOB
 permit ip 192.168.99.0 0.0.0.255 192.168.100.0 0.0.0.255
 remark Permit OOB to PAWs
 permit ip 192.168.100.0 0.0.0.255 192.168.99.0 0.0.0.255
 remark Deny all other VLANs to OOB
 deny   ip any 192.168.100.0 0.0.0.255
 remark Permit OOB to any (for mgmt reachability)
 permit ip 192.168.100.0 0.0.0.255 any

3.5 ROUTER-PROTECT

Protects Router inside VLAN (90) while allowing PAWs.
cisco

ip access-list extended ROUTER-PROTECT
 remark Permit PAWs to Router inside VLAN
 permit ip 192.168.99.0 0.0.0.255 192.168.90.0 0.0.0.255
 remark Permit Router inside VLAN to PAWs
 permit ip 192.168.90.0 0.0.0.255 192.168.99.0 0.0.0.255
 remark Deny all other VLANs to Router inside VLAN
 deny   ip any 192.168.90.0 0.0.0.255
 remark Permit Router inside VLAN to any (for routing)
 permit ip 192.168.90.0 0.0.0.255 any

================================================================================
4. ACL Application (WS‑3850 SVIs)

================================================================================
Planned application (do not apply until tested):
cisco

interface Vlan10
 description Identity Services
 ip access-group IDENTITY-PROTECT in

interface Vlan20
 description ESXi Hosts
 ip access-group ESXI-PROTECT in

interface Vlan100
 description Management / OOB
 ip access-group OOB-PROTECT in

interface Vlan90
 description WAN Edge / Router Inside
 ip access-group ROUTER-PROTECT in

No ACL is applied on:
cisco

interface Vlan99
 description PAWs (Tier-0 Admin)
 ! No ACL inbound; PAWs must reach all VLANs

================================================================================
5. Notes

================================================================================

    ACLs are designed for WS‑3850 only; 891F ACLs are intentionally avoided.

    PAWs (VLAN 99) retain full routed access to all VLANs.

    Identity, ESXi, OOB, and Router VLANs are protected from non‑PAW traffic.

    This document must remain aligned with:

        homelab-vlan-plan.md

        homelab-addressing-plan.md

        homelab-device-vlan-mapping.md

        homelab-routing-plan.md

================================================================================
END OF DOCUMENT
================================================================================