# Network Physical Layer — theITchef Homelab
Version: 2026‑07‑03  
Location: Upplands Väsby, Stockholm County, Sweden  
Author: Ioannis Mintzivyris

---

## 1. Purpose

This document defines the **physical network identity** of every device in the homelab:

- NIC ports  
- MAC addresses  
- Management interfaces  
- IP placeholders  
- Reset/default state notes  

No VLANs, routing, or addressing plan are included here.

---

## 2. Servers — Physical Network Identity

---

### itc‑uvy‑dc01 — Dell PowerEdge T330
**OS:** Windows Server 2025 Standard (planned)  
**State:** Reset to defaults

#### NICs — Broadcom BCM5720
| Physical Port | MAC Address |
|---------------|-------------|
| NIC1 | 50:9A:4C:8C:A4:CF |
| NIC2 | 50:9A:4C:8C:A4:D0 |

#### Management
| Interface | MAC Address |
|----------|-------------|
| iDRAC8 | 50:9A:4C:8C:A4:D1 |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| DC01 Host IP | `TBD_DC01_IP` |
| DC01 iDRAC | `TBD_DC01_IDRAC_IP` |

---

### itc‑uvy‑esxi01 — Dell PowerEdge R620
**OS:** ESXi 8.0  
**State:** Minimal config from installer

#### NICs — Onboard Intel I350‑t rNDC (vmnic0–vmnic3)
| Physical Port | ESXi Interface | MAC Address |
|---------------|----------------|-------------|
| LOM1 | vmnic0 | 88:CA:3A:5F:9C:7C |
| LOM2 | vmnic1 | 88:CA:3A:5F:9C:7D |
| LOM3 | vmnic2 | 88:CA:3A:5F:9C:7E |
| LOM4 | vmnic3 | 88:CA:3A:5F:9C:7F |

#### NICs — PCIe Intel Gigabit ET Quad Port (Slot 3)
| Physical Port | ESXi Interface | MAC Address |
|---------------|----------------|-------------|
| LOM5 | — | 00:B2:1B:9B:B0:59 |
| LOM6 | — | 00:B2:1B:9B:B0:5A |
| LOM7 | — | 00:B2:1B:9B:B0:5C |
| LOM8 | — | 00:B2:1B:9B:B0:5D |

#### Management
| Interface | MAC Address |
|----------|-------------|
| iDRAC7 | 74:86:7A:CE:68:B2 |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| ESXi01 Host IP | `TBD_ESXI01_IP` |
| ESXi01 mgmt vmk0 | `TBD_ESXI01_MGMT_IP` |
| ESXi01 iDRAC | `TBD_ESXI01_IDRAC_IP` |

---

### itc‑uvy‑esxi02 — Dell PowerEdge R620
**OS:** TBD  
**State:** Reset to defaults

#### NICs — Broadcom BCM5720
| Physical Port | MAC Address |
|---------------|-------------|
| LOM1 | 90:B1:1C:3D:C2:B1 |
| LOM2 | 90:B1:1C:3D:C2:B2 |
| LOM3 | 90:B1:1C:3D:C2:B3 |
| LOM4 | 90:B1:1C:3D:C2:B4 |

#### Management
| Interface | MAC Address |
|----------|-------------|
| iDRAC7 | E0:DB:55:1F:E2:9A |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| ESXi02 Host IP | `TBD_ESXI02_IP` |
| ESXi02 mgmt vmk0 | `TBD_ESXI02_MGMT_IP` |
| ESXi02 iDRAC | `TBD_ESXI02_IDRAC_IP` |

---

### itc‑uvy‑ms‑01 — HPE ProLiant DL360 Gen9
**OS:** Windows Server 2025 Datacenter  
**State:** Reset to defaults

#### NICs — Broadcom 331i
| Physical Port | MAC Address |
|---------------|-------------|
| eth0 | 94:57:A5:58:63:38 |
| eth1 | 94:57:A5:58:63:39 |
| eth2 | 94:57:A5:58:63:3A |
| eth3 | 94:57:A5:58:63:3B |

#### Management
| Interface | MAC Address |
|----------|-------------|
| iLO4 | 94:57:A5:69:B2:86 |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| MS01 Host IP | `TBD_MS01_IP` |
| MS01 iLO | `TBD_MS01_ILO_IP` |

---

## 3. Network Devices — Physical Network Identity

---

### Cisco WS‑C3850‑48P — Core Switch
**State:** Reset to defaults  
**Base MAC:** 4C:71:0C:0F:11:80

#### VLAN / SVI
| Interface | MAC Address |
|----------|-------------|
| VLAN SVI (VLAN1) | 4C:71:0C:0F:11:C7 |

#### Management Port
| Interface | MAC Address |
|----------|-------------|
| Mgmt | 4C:71:0C:0F:11:80 |

#### GigabitEthernet Interfaces (Gi1/0/1 → Gi1/0/48)
| Interface | MAC Address |
|----------|-------------|
| Gi1/0/1 | 4C:71:0C:0F:11:81 |
| Gi1/0/2 | 4C:71:0C:0F:11:82 |
| Gi1/0/3 | 4C:71:0C:0F:11:83 |
| Gi1/0/4 | 4C:71:0C:0F:11:84 |
| Gi1/0/5 | 4C:71:0C:0F:11:85 |
| Gi1/0/6 | 4C:71:0C:0F:11:86 |
| Gi1/0/7 | 4C:71:0C:0F:11:87 |
| Gi1/0/8 | 4C:71:0C:0F:11:88 |
| Gi1/0/9 | 4C:71:0C:0F:11:89 |
| Gi1/0/10 | 4C:71:0C:0F:11:8A |
| Gi1/0/11 | 4C:71:0C:0F:11:8B |
| Gi1/0/12 | 4C:71:0C:0F:11:8C |
| Gi1/0/13 | 4C:71:0C:0F:11:8D |
| Gi1/0/14 | 4C:71:0C:0F:11:8E |
| Gi1/0/15 | 4C:71:0C:0F:11:8F |
| Gi1/0/16 | 4C:71:0C:0F:11:90 |
| Gi1/0/17 | 4C:71:0C:0F:11:91 |
| Gi1/0/18 | 4C:71:0C:0F:11:92 |
| Gi1/0/19 | 4C:71:0C:0F:11:93 |
| Gi1/0/20 | 4C:71:0C:0F:11:94 |
| Gi1/0/21 | 4C:71:0C:0F:11:95 |
| Gi1/0/22 | 4C:71:0C:0F:11:96 |
| Gi1/0/23 | 4C:71:0C:0F:11:97 |
| Gi1/0/24 | 4C:71:0C:0F:11:98 |
| Gi1/0/25 | 4C:71:0C:0F:11:99 |
| Gi1/0/26 | 4C:71:0C:0F:11:9A |
| Gi1/0/27 | 4C:71:0C:0F:11:9B |
| Gi1/0/28 | 4C:71:0C:0F:11:9C |
| Gi1/0/29 | 4C:71:0C:0F:11:9D |
| Gi1/0/30 | 4C:71:0C:0F:11:9E |
| Gi1/0/31 | 4C:71:0C:0F:11:9F |
| Gi1/0/32 | 4C:71:0C:0F:11:A0 |
| Gi1/0/33 | 4C:71:0C:0F:11:A1 |
| Gi1/0/34 | 4C:71:0C:0F:11:A2 |
| Gi1/0/35 | 4C:71:0C:0F:11:A3 |
| Gi1/0/36 | 4C:71:0C:0F:11:A4 |
| Gi1/0/37 | 4C:71:0C:0F:11:A5 |
| Gi1/0/38 | 4C:71:0C:0F:11:A6 |
| Gi1/0/39 | 4C:71:0C:0F:11:A7 |
| Gi1/0/40 | 4C:71:0C:0F:11:A8 |
| Gi1/0/41 | 4C:71:0C:0F:11:A9 |
| Gi1/0/42 | 4C:71:0C:0F:11:AA |
| Gi1/0/43 | 4C:71:0C:0F:11:AB |
| Gi1/0/44 | 4C:71:0C:0F:11:AC |
| Gi1/0/45 | 4C:71:0C:0F:11:AD |
| Gi1/0/46 | 4C:71:0C:0F:11:AE |
| Gi1/0/47 | 4C:71:0C:0F:11:AF |
| Gi1/0/48 | 4C:71:0C:0F:11:B0 |

#### TenGigabitEthernet Interfaces (Te1/1/1 → Te1/1/4)
| Interface | MAC Address |
|----------|-------------|
| Te1/1/1 | 4C:71:0C:0F:11:B5 |
| Te1/1/2 | 4C:71:0C:0F:11:B6 |
| Te1/1/3 | 4C:71:0C:0F:11:B7 |
| Te1/1/4 | 4C:71:0C:0F:11:B8 |

---

### Cisco WS‑C3560CG‑8PC‑S — OOB Switch
**State:** Reset to power‑on defaults  
**Base MAC:** 38:1C:1A:F8:9F:80

#### VLAN / SVI
| Interface | MAC Address |
|----------|-------------|
| VLAN SVI (VLAN1) | 38:1C:1A:F8:9F:C0 |

#### GigabitEthernet Interfaces
| Interface | MAC Address |
|----------|-------------|
| Gi0/1 | 38:1C:1A:F8:9F:81 |
| Gi0/2 | 38:1C:1A:F8:9F:82 |
| Gi0/3 | 38:1C:1A:F8:9F:83 |
| Gi0/4 | 38:1C:1A:F8:9F:84 |
| Gi0/5 | 38:1C:1A:F8:9F:85 |
| Gi0/6 | 38:1C:1A:F8:9F:86 |
| Gi0/7 | 38:1C:1A:F8:9F:87 |
| Gi0/8 | 38:1C:1A:F8:9F:88 |
| Gi0/9 | 38:1C:1A:F8:9F:89 |
| Gi0/10 | 38:1C:1A:F8:9F:8A |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| 3560CG mgmt VLAN SVI | `TBD_3560CG_MGMT_IP` |

---

### itc‑uvy‑rtr01 — Cisco C891F‑K9
**Role:** Edge Router  
**OS:** Cisco IOS 15.4(3)M3  
**State:** WAN‑only, not factory reset

#### Base / CPU / Control Plane
| Component | MAC Address |
|----------|-------------|
| CPU / Control (PQII_PRO_UEC) | 00:BE:75:2D:BB:6E |

#### Layer‑3 / SVI Interfaces
| Interface | MAC Address | Notes |
|----------|-------------|-------|
| VLAN SVI (LAN, 10.10.10.254/24) | 00:BE:75:2D:BB:64 | EtherSVI |
| Additional SVI | 00:BE:75:2D:BB:64 | Same MAC reused |

#### GigabitEthernet Interfaces
| Interface (GiX) | MAC Address |
|-----------------|-------------|
| Gi — #1 | 00:BE:75:2D:BB:65 |
| Gi — #2 | 00:BE:75:2D:BB:66 |
| Gi — #3 | 00:BE:75:2D:BB:67 |
| Gi — #4 | 00:BE:75:2D:BB:68 |
| Gi — #5 | 00:BE:75:2D:BB:69 |
| Gi — #6 | 00:BE:75:2D:BB:6A |
| Gi — #7 | 00:BE:75:2D:BB:6B |
| Gi — #8 | 00:BE:75:2D:BB:6C |

#### WAN / Uplink
| Interface | MAC Address | Notes |
|----------|-------------|-------|
| WAN (PQ3_TSEC, 85.228.45.152/21) | 00:BE:75:2D:BB:76 | Internet‑facing |

#### IP Placeholders
| Purpose | Placeholder |
|---------|-------------|
| LAN Gateway IP | 10.10.10.254 |
| WAN IP | 85.228.45.152 |

---

## 4. Workstations / PAWs — Physical Network Identity

### PAW‑01 — ASUS PN52
| Interface | MAC Address |
|----------|-------------|
| Ethernet | `TBD_PAW01_ETH_MAC` |
| Wi‑Fi | `TBD_PAW01_WIFI_MAC` |

### PAW‑02 — Lenovo T470s
| Interface | MAC Address |
|----------|-------------|
| Ethernet | `TBD_PAW02_ETH_MAC` |
| Wi‑Fi | `TBD_PAW02_WIFI_MAC` |

---

## 5. Management Interfaces Summary

| Device | Interface | MAC Address |
|--------|-----------|-------------|
| DC01 | iDRAC8 | 50:9A:4C:8C:A4:D1 |
| ESXi01 | iDRAC7 | 74:86:7A:CE:68:B2 |
| ESXi02 | iDRAC7 | E0:DB:55:1F:E2:9A |
| MS01 | iLO4 | 94:57:A5:69:B2:86 |
| 3850 | Mgmt | 4C:71:0C:0F:11:80 |
| 3560CG | Mgmt SVI | 38:1C:1A:F8:9F:C0 |
| 891F | WAN | 00:BE:75:2D:BB:76 |

---

## 6. Notes

- All IPs are placeholders until the addressing plan is created.  
- ESXi01 and DC01 are partially configured; all other devices are reset or WAN‑only.  
- Switch MACs follow linear ASIC allocation.  
- This document includes **all rack devices** and **all network‑connected devices**.

---

**End of NetworkPhysicalLayer.md**
