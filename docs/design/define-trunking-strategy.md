# Trunking Strategy
Version: 2026‑07‑07

## 1. Purpose
Authoritative trunking model for all switches and hosts.  
Foundation for VLAN plan, port mapping, routing, ACLs, and ESXi design.

---

## 2. Trunking Model
- **802.1Q trunks everywhere**  
- **No dynamic trunking (DTP disabled)**  
- **Native VLAN = none (tag all)**  
- **Allowed VLANs = full VLAN plan**  
- **DMZ VLAN only on firewall-facing trunks**  
- **Storage VLAN only on ESXi + storage switches**

---

## 3. Allowed VLAN Set
`10,20,30,40,50,60,70,80,90,100`

---

## 4. Trunk Types

### Core ↔ Access
- Mode: `trunk`
- Allowed: all VLANs except DMZ unless required
- Native: none

### Core ↔ ESXi
- Mode: `trunk`
- Allowed: 10,20,30,40,50
- Native: none

### Core ↔ Firewall
- Mode: `trunk`
- Allowed: 10,20,40,50,80
- Native: none

---

## 5. Cisco Configuration Template

```text
interface GiX/X
 description <DEVICE> <ROLE>
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,100
 switchport trunk native vlan none
 switchport nonegotiate
 spanning-tree portfast trunk

6. ESXi Uplink Requirements

    vmnic0 → MGMT trunk

    vmnic1 → vMotion trunk

    vmnic2 → Storage trunk

    vmnic3 → VM Networks trunk

    All tagged, no native VLAN

7. Validation

    show interfaces trunk

    show spanning-tree interface

    ESXi: esxcli network nic list

    ESXi: esxcli network vswitch standard list