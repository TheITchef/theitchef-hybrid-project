# Port Mapping Procedure
## Hybrid Homelab — Physical Cabling & Switch Port Documentation

---

## 1. Purpose
This document defines the **Port Mapping Procedure** for the hybrid homelab.  
It ensures consistent, validated mapping between:

- Device NICs  
- Patch panel ports  
- Switch ports  
- VLAN assignments  
- Trunking configuration  

This procedure is required before:
- Inter‑VLAN routing validation  
- ESXi deployment  
- Hyper‑V deployment  
- Identity deployment  
- PKI deployment  
- ADFS/WAP deployment  
- Azure AD Connect deployment  

---

## 2. Scope
This procedure covers:
- Physical NIC → Patch Panel mapping  
- Patch Panel → Switch Port mapping  
- Switch Port → VLAN/Trunk mapping  
- OOB port mapping  
- Router Inside port mapping  
- Validation steps  

---

## 3. Device NIC → Patch Panel Mapping

### 3.1 ESXi01 (R620‑01)
| NIC | Patch Panel Port | Switch Port | Notes |
|-----|------------------|-------------|-------|
| vmnic0 | TBD | TBD | Management |
| vmnic1 | TBD | TBD | vMotion |
| vmnic2 | TBD | TBD | VM Network |
| vmnic3 | TBD | TBD | VM Network |

---

### 3.2 ESXi02 (R620‑02)
| NIC | Patch Panel Port | Switch Port | Notes |
|-----|------------------|-------------|-------|
| vmnic0 | TBD | TBD | Management |
| vmnic1 | TBD | TBD | vMotion |
| vmnic2 | TBD | TBD | VM Network |
| vmnic3 | TBD | TBD | VM Network |

---

### 3.3 Hyper‑V Host (MS01)
| NIC | Patch Panel Port | Switch Port | Notes |
|-----|------------------|-------------|-------|
| NIC1 | TBD | TBD | Management |
| NIC2 | TBD | TBD | VM Network |
| NIC3 | TBD | TBD | VM Network |
| NIC4 | TBD | TBD | Reserved |

---

### 3.4 DC01 (T330)
| NIC | Patch Panel Port | Switch Port | Notes |
|-----|------------------|-------------|-------|
| NIC1 | TBD | TBD | Identity VLAN |
| NIC2 | TBD | TBD | Reserved |

---

### 3.5 PAWs (PN52 / T470s)
| Device | NIC | Patch Panel Port | Switch Port | Notes |
|--------|-----|------------------|-------------|-------|
| PN52 | NIC1 | TBD | TBD | PAW VLAN |
| T470s | NIC1 | TBD | TBD | PAW VLAN |

---

### 3.6 OOB Management (C3560CG)
| Device | Port | Patch Panel Port | Switch Port | Notes |
|--------|-------|------------------|-------------|-------|
| C3560CG | Gi0/1–Gi0/8 | TBD | TBD | OOB VLAN |

---

### 3.7 Router Inside (Cisco 891F)
| Router Port | Patch Panel Port | Switch Port | Notes |
|-------------|------------------|-------------|-------|
| FE0/1 | TBD | TBD | Inside VLAN (90) |
| FE0/2 | TBD | TBD | Reserved |
| FE0/3 | TBD | TBD | Reserved |
| FE0/4 | TBD | TBD | Reserved |

---

## 4. Patch Panel → Switch Port Mapping

| Patch Panel Port | Switch Port | Connected Device | Notes |
|------------------|-------------|------------------|-------|
| 1 | TBD | ESXi01 vmnic0 | |
| 2 | TBD | ESXi01 vmnic1 | |
| 3 | TBD | ESXi01 vmnic2 | |
| 4 | TBD | ESXi01 vmnic3 | |
| 5 | TBD | ESXi02 vmnic0 | |
| 6 | TBD | ESXi02 vmnic1 | |
| 7 | TBD | ESXi02 vmnic2 | |
| 8 | TBD | ESXi02 vmnic3 | |
| 9 | TBD | MS01 NIC1 | |
| 10 | TBD | MS01 NIC2 | |
| 11 | TBD | MS01 NIC3 | |
| 12 | TBD | MS01 NIC4 | |
| 13 | TBD | DC01 NIC1 | |
| 14 | TBD | DC01 NIC2 | |
| 15 | TBD | PN52 | |
| 16 | TBD | T470s | |
| 17 | TBD | C3560CG uplink | |
| 18 | TBD | Cisco 891F FE0/1 | |

---

## 5. Switch Port → VLAN/Trunk Mapping

| Switch Port | Mode | VLAN(s) | Notes |
|-------------|------|---------|-------|
| Gi1/0/1 | Access | 20 | ESXi01 mgmt |
| Gi1/0/2 | Access | 20 | ESXi01 vMotion |
| Gi1/0/3 | Trunk | 30 | ESXi01 VM Network |
| Gi1/0/4 | Trunk | 30 | ESXi01 VM Network |
| Gi1/0/5 | Access | 20 | ESXi02 mgmt |
| Gi1/0/6 | Access | 20 | ESXi02 vMotion |
| Gi1/0/7 | Trunk | 30 | ESXi02 VM Network |
| Gi1/0/8 | Trunk | 30 | ESXi02 VM Network |
| Gi1/0/9 | Access | 10 | DC01 |
| Gi1/0/10 | Access | 99 | PAW |
| Gi1/0/11 | Access | 100 | OOB |
| Gi1/0/12 | Access | 90 | Router Inside |

---

## 6. Validation Procedure

### 6.1 Physical Validation
- Confirm cable color  
- Confirm patch panel port  
- Confirm switch port  
- Confirm device NIC  
- Confirm labeling  

### 6.2 Logical Validation
- Confirm VLAN assignment  
- Confirm trunking  
- Confirm routing reachability  
- Confirm ACL enforcement  

### 6.3 Documentation Validation
- Update this `.md`  
- Update Kanban  
- Update diagrams  

---

## 7. Acceptance Criteria
- All NICs mapped  
- All patch panel ports mapped  
- All switch ports mapped  
- All VLAN assignments validated  
- Documentation complete  
