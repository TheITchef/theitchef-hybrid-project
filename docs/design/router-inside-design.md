# Router Inside Design (Cisco 891F)
Version: 2026‑07‑07  
Author: Ioannis Mintzivyris

## 1. Purpose
Define the inside‑network design for the Cisco 891F WAN edge router, including interface roles, IP addressing, routing behavior, firewall adjacency, and integration with the WS‑3850 core switch.

The design is based on:
- Hybrid Homelab Project Document (Cisco 891F = WAN edge)  
- Physical cabling observations (FE0/1–FE0/4 present on router)  

## 2. Device Overview
- **Model:** Cisco 891F  
- **Role:** WAN edge router  
- **Inside interfaces:** FE0/1, FE0/2, FE0/3, FE0/4  
  (Confirmed in cabling log: “Router Inside (Cisco 891F) Cabling”)

## 3. Logical Placement

+----------------------+
|      Internet        |
+----------+-----------+
|
|
+----------v-----------+
|      Cisco 891F      |
|     WAN Edge Router  |
+----------+-----------+
|
|
+----------v-----------+
|       Firewall       |
| Inside: 10.10.50.253 |
+----------+-----------+
|
|
+----------v-----------+
|     WS-3850 Core     |
+----------------------+
Code


## 4. Inside Interface Design

### 4.1 Inside VLAN Gateway
- **Inside network:** 10.10.50.0/24  
- **Router inside IP:** 10.10.50.254  
- **Firewall inside IP:** 10.10.50.253  
- **Core switch SVI:** 10.10.50.1  

### 4.2 Interface Assignment

| Interface | Role          | IP               | Notes                         |
|----------|---------------|------------------|-------------------------------|
| FE0/1    | Inside LAN     | 10.10.50.254/24  | Primary inside gateway        |
| FE0/2    | Reserved       | —                | Future segmentation           |
| FE0/3    | Reserved       | —                | Future segmentation           |
| FE0/4    | Reserved       | —                | Future segmentation           |

## 5. Routing Design

### 5.1 Static Routes

ip route 0.0.0.0 0.0.0.0 <ISP-NEXT-HOP>
ip route 10.10.0.0 255.255.0.0 10.10.50.1
Code


### 5.2 Firewall Relationship
- Router sends all internal traffic to firewall inside interface  
- Firewall performs NAT + security inspection  
- Router does **not** perform NAT for internal VLANs  
- Router does **not** perform inter‑VLAN routing  

## 6. DHCP Relay
DHCP server resides in Infrastructure VLAN (50).

interface FE0/1
ip helper-address 10.10.50.11
Code


## 7. Security Controls
- No direct DMZ routing  
- No inter‑VLAN routing on router  
- ACLs only for WAN edge protection  
- LAN security handled by WS‑3850 + firewall  
- Router inside interface is a **trusted boundary** but not a routing decision point  

## 8. Cabling Reference
From cabling log (Router Inside section):

> FE0/1  
> FE0/2  
> FE0/3  
> FE0/4  


These ports form the physical basis of the inside design.

## 9. Notes
- Router is WAN edge only — not a core router  
- All internal routing is performed by WS‑3850  
- Firewall is the security boundary between router and core  
- Design aligns with VLAN, addressing, routing, ACL, and monitoring architecture  