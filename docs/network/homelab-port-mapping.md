# homelab-port-mapping
Version: 2026-07-03  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

================================================================================
## 1. Purpose
================================================================================
This document defines the physical port-to-device mapping for all switches in the
homelab. It ensures consistent documentation of access ports, trunk ports, VLAN
assignments, and rack connectivity.

This mapping supports:
- VLAN plan
- Addressing plan
- Device-to-VLAN mapping
- Trunking strategy
- OOB management design

================================================================================
## 2. Switch Inventory
================================================================================

### WS-C3850-48T-L (Core Switch)
Role: Core L3 switch  
Location: Rack position (core)

### WS-C3560CG-8PC-S (OOB Switch)
Role: OOB + PAW access  
Location: Rack position (top-of-rack)

### Cisco 891F (Router)
Role: WAN edge  
Location: Rack position (edge)

================================================================================
## 3. Port Mapping — WS-C3850 (Core)
================================================================================

| Port | Mode | VLAN(s) | Connected Device | Notes |
|------|------|---------|------------------|-------|
| Gi1/0/1 | trunk | 1,10,20,30,90,99,100 | C3560CG Gi0/1 | OOB uplink |
| Gi1/0/2 | trunk | 1,90 | Cisco 891F | Router inside interface |
| Gi1/0/3 | trunk | 1,10,20,30,99,100 | ESXi01 vmnic | Hypervisor uplink |
| Gi1/0/4 | trunk | 1,10,20,30,99,100 | ESXi02 vmnic | Hypervisor uplink |
| Gi1/0/5 | trunk | 1,10,20,30,99,100 | Hyper-V DL360 | Hyper-V uplink |
| Gi1/0/6 | access | 10 | DC01 | Identity zone |
| Gi1/0/7 | access | 30 | MS01 | VM workloads |
| Gi1/0/8 | access | 100 | iDRAC DC01 | OOB mgmt |
| Gi1/0/9 | access | 100 | iDRAC ESXi01 | OOB mgmt |
| Gi1/0/10 | access | 100 | iDRAC ESXi02 | OOB mgmt |
| Gi1/0/11 | access | 100 | iLO DL360 | OOB mgmt |
| Gi1/0/12 | access | 10 | ADFS/WAP | Identity zone |
| Gi1/0/13 | access | 10 | PKI SubCA | Identity zone |
| Gi1/0/14 | access | 30 | VM workloads | General VMs |
| Gi1/0/15 | access | 30 | VM workloads | General VMs |

*(Continue filling remaining ports as needed.)*

================================================================================
## 4. Port Mapping — WS-C3560CG (OOB + PAW)
================================================================================

| Port | Mode | VLAN | Connected Device | Notes |
|------|------|------|------------------|-------|
| Gi0/1 | trunk | 1,10,20,30,90,99,100 | 3850 Gi1/0/1 | Uplink to core |
| Gi0/2 | access | 99 | PN52 | PAW |
| Gi0/3 | access | 99 | T470s | PAW |
| Gi0/4 | access | 100 | OOB device | mgmt |
| Gi0/5 | access | 100 | OOB device | mgmt |
| Gi0/6 | access | 99 | PAW | Admin workstation |
| Gi0/7 | access | 99 | PAW | Admin workstation |
| Gi0/8 | access | 100 | Spare OOB | mgmt |

================================================================================
## 5. Port Mapping — Cisco 891F (Router)
================================================================================

| Port | Mode | VLAN | Connected Device | Notes |
|------|------|------|------------------|-------|
| Gi0/0 | WAN | n/a | ISP | WAN uplink |
| Gi0/1 | trunk | 1,90 | 3850 Gi1/0/2 | Inside interface (VLAN 90) |

================================================================================
## 6. Notes
================================================================================
- PAWs connect to the 3560CG on VLAN 99 and reach all VLANs via L3 routing on the 3850.
- Router inside interface is isolated in VLAN 90 to reduce broadcast exposure.
- All OOB management interfaces are placed in VLAN 100.
- ESXi hosts use trunk uplinks carrying VLANs 10,20,30,99,100.
- Native VLAN 1 is kept clean and unused for production traffic.
- This document must remain synchronized with:
  - homelab-vlan-plan.md
  - homelab-addressing-plan.md
  - homelab-device-vlan-mapping.md

================================================================================
END OF DOCUMENT
================================================================================
