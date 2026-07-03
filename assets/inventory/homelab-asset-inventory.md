# Asset Inventory — theITchef Homelab
Version: 2026‑07‑03  
Location: Upplands Väsby, Stockholm County, Sweden  
Author: Ioannis Mintzivyris

---

## 1. Servers

### itc‑uvy‑dc01 — Dell PowerEdge T330
**Role:** Primary Domain Controller  
**Hypervisor:** None  
**Operating System:** Windows Server 2025 Standard (AD DS)

#### Hardware
| Component | Details |
|----------|---------|
| Model | Dell PowerEdge T330 |
| CPU | Intel Xeon E3‑1220 v6 (4C/4T) |
| Memory | 32GB DDR4 ECC |
| Storage | 2× HDD (RAID1) |
| RAID Controller | Dell PERC |
| iDRAC | iDRAC8 Enterprise |
| NIC | 2× 1GbE |
| PSU | 495W |

---

### itc‑uvy‑esxi01 — Dell PowerEdge R620
**Role:** ESXi Host  
**Hypervisor:** VMware ESXi 8.0  
**Operating System:** ESXi 8.0 (bare‑metal)

#### Hardware
| Component | Details |
|----------|---------|
| Model | Dell PowerEdge R620 |
| CPU | 2× Intel Xeon E5‑2660 v2 (20C/40T total) |
| Memory | 192GB DDR3 ECC |
| Storage | Samsung SSD 870 (RAID0) |
| RAID Controller | PERC H710 Mini |
| iDRAC | iDRAC7 Enterprise |
| NIC | 4× 1GbE |
| PSU | Dual redundant |

---

### itc‑uvy‑esxi02 — Dell PowerEdge R620
**Role:** ESXi Host (planned)  
**Hypervisor:** TBD  
**Operating System:** TBD

#### Hardware
| Component | Details |
|----------|---------|
| Model | Dell PowerEdge R620 |
| CPU | 2× Intel Xeon E5‑2660 v2 |
| Memory | 192GB DDR3 ECC |
| Storage | Samsung SSD 870 (RAID0) |
| RAID Controller | PERC H710 Mini |
| iDRAC | iDRAC7 Enterprise |
| NIC | 4× 1GbE |
| PSU | Dual redundant |

---

### itc‑uvy‑ms‑01 — HPE ProLiant DL360 Gen9
**Role:** Hyper‑V Host  
**Hypervisor:** Microsoft Hyper‑V  
**Operating System:** Windows Server 2025 Datacenter

#### System Summary
| Field | Value |
|-------|-------|
| Manufacturer | HP |
| Model | ProLiant DL360 Gen9 |
| BIOS | P89 (2024‑08‑29) |
| iLO | iLO 4 — 2.82 |

#### CPU
| Socket | Model | Cores | Threads |
|--------|--------|--------|---------|
| CPU 1 | Intel Xeon E5‑2630 v3 | 8 | 16 |
| CPU 2 | Intel Xeon E5‑2630 v3 | 8 | 16 |

**Total:** 16C / 32T  
**Base Clock:** 2.40GHz  
**Max Turbo:** 4.00GHz  

#### Memory
| Field | Value |
|-------|-------|
| Total | 256GB DDR4 LRDIMM |
| Type | PC4‑2133L‑15 |
| ECC | Advanced ECC |

#### Storage
| Component | Details |
|----------|---------|
| RAID Controller | HP Smart Array P440ar |
| Disk | Samsung SSD 870 — 1TB |
| RAID | RAID0 |

#### Networking
| Interface | MAC | Notes |
|-----------|------|-------|
| eth0 | 94:57:A5:58:63:38 | Inactive |
| eth1 | 94:57:A5:58:63:39 | Inactive |
| eth2 | 94:57:A5:58:63:3A | Active |
| eth3 | 94:57:A5:58:63:3B | Inactive |

#### iLO
| Field | Value |
|-------|--------|
| MAC | 94:57:A5:69:B2:86 |
| DNS | itc‑uvy‑ms‑01 |

---

## 2. Workstations / PAWs

### PAW‑01 — ASUS PN52
| Component | Details |
|----------|---------|
| Role | Privileged Access Workstation |
| OS | Windows 11 |
| CPU | AMD Ryzen |
| Memory | 32GB |
| Storage | NVMe SSD |
| NIC | 1GbE + Wi‑Fi |

---

### PAW‑02 — Lenovo T470s
| Component | Details |
|----------|---------|
| Role | Secondary PAW |
| OS | Ubuntu Linux |
| CPU | Intel Core i7 |
| Memory | 16GB |
| Storage | SSD |
| NIC | 1GbE + Wi‑Fi |

---

## 3. Network

### Switches

#### Cisco WS‑C3850‑48T
| Component | Details |
|----------|---------|
| Model | Catalyst 3850‑48T |
| Ports | 48× 1GbE |
| Uplink | 4× SFP |
| PSU | Redundant |
| Role | Core Switch |

#### Cisco WS‑C3560CG‑8PC
| Component | Details |
|----------|---------|
| Model | Catalyst 3560CG‑8PC |
| Ports | 8× 1GbE PoE |
| Uplink | 2× SFP |
| Role | OOB / Management Switch |

### Router

#### Cisco 891F
| Component | Details |
|----------|---------|
| Model | Cisco 891F |
| WAN | 1× GE |
| LAN | 8× GE |
| Role | Edge Router |

---

## 4. Power Distribution

### PDU‑01 — HPE Modular PDU Control Unit (Vertical)
| Field | Value |
|-------|-------|
| Part Number | 228481‑006 |
| Spare Part | 417583‑001 |
| Rating | 16A, 200–240VAC, 1‑phase |

### PDU‑02 — HPE Modular PDU Control Unit (Vertical)
| Field | Value |
|-------|-------|
| Part Number | 228481‑006 |
| Spare Part | 417583‑001 |
| Rating | 16A, 200–240VAC, 1‑phase |

---

## 5. Rack Layout (42U)

| U‑Position | Device |
|-----------|---------|
| U38 | Cisco 891F |
| U37 | Empty |
| U36 | Cisco WS‑C3560CG‑8PC |
| U35 | Empty |
| U34 | 24‑Port Patch Panel |
| U33 | Cisco WS‑C3850‑48T |
| U32–U15 | Empty |
| U14 | itc‑uvy‑esxi01 — Dell R620 |
| U13 | itc‑uvy‑esxi02 — Dell R620 |
| U12 | itc‑uvy‑ms‑01 — HPE DL360 Gen9 |
| U11–U01 | itc‑uvy‑dc01 — Dell T330 |

---

## 6. Notes & Exclusions
- Cabling excluded  
- VLANs/trunks excluded  
- VM inventory excluded  
- Storage design excluded  
- Network design excluded  
- All IP information intentionally omitted  

---

**End of AssetInventory.md**
