# ESXi01 Networking Design
Version: 2026‑07‑07  
Host: esxi01.lab.theitchef.com  

---

## 1. Purpose
Define the complete network configuration for ESXi01, aligned with VLAN Plan, Trunking Strategy, VM Placement Plan, and Cisco switch configuration.

---

## 2. NIC Inventory
- vmnic0 → NIC.Integrated.1‑1‑1  
- vmnic1 → NIC.Integrated.1‑2‑1  
- vmnic2 → NIC.Integrated.1‑3‑1  
- vmnic3 → NIC.Integrated.1‑4‑1  

---

## 3. Physical Mapping
- vmnic0 → Patch panel port X → Switch Gi0/1 (trunk)  
- vmnic1 → Patch panel port Y → Switch Gi0/2 (trunk)  
- vmnic2 → Patch panel port Z → Switch Gi0/3 (trunk)  
- vmnic3 → Patch panel port W → Switch Gi0/4 (trunk)  

(Replace X/Y/Z/W with actual cabling values from observation log.)

---

## 4. VLAN Assignments
- Management VLAN: `VLAN 10`  
- vMotion VLAN: `VLAN 20`  
- Storage VLAN: `VLAN 30` (optional)  
- Server VM VLAN: `VLAN 40`  
- Infra VM VLAN: `VLAN 50`  

(Align numbers with your VLAN Plan.)

---

## 5. vSwitch Design

### vSwitch0 — Management
- Uplink: vmnic0  
- Port group: `PG-MGMT` (VLAN 10)  
- VMkernel: `vmk0` (Management)  

### vSwitch1 — vMotion
- Uplink: vmnic1  
- Port group: `PG-VMOTION` (VLAN 20)  
- VMkernel: `vmk1` (vMotion)  

### vSwitch2 — Storage (optional)
- Uplink: vmnic2  
- Port group: `PG-STORAGE` (VLAN 30)  
- VMkernel: `vmk2` (Storage)  

### vSwitch3 — VM Networks
- Uplink: vmnic3  
- Port groups:
  - `PG-SRV-VM` (VLAN 40)  
  - `PG-INFRA-VM` (VLAN 50)  

---

## 6. Cisco Switch Trunking (Example)

```text
interface GigabitEthernet0/1
 description ESXi01 vmnic0 MGMT
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50

interface GigabitEthernet0/2
 description ESXi01 vmnic1 VMOTION
 switchport mode trunk
 switchport trunk allowed vlan 20

interface GigabitEthernet0/3
 description ESXi01 vmnic2 STORAGE
 switchport mode trunk
 switchport trunk allowed vlan 30

interface GigabitEthernet0/4
 description ESXi01 vmnic3 VM-NET
 switchport mode trunk
 switchport trunk allowed vlan 40,50
