---
title: Define Port Mapping — Homelab Hybrid Project
orientation: landscape
---

# Define Port Mapping — Homelab Structured Cabling

This document converts the verified physical cabling into a logical port mapping design.  
It aligns with the trunking strategy and current device roles.

---

## 1. WS‑3850 — Access & Uplink Port Mapping

| Switch Port | Connected Device | Connected NIC | Patch Panel | Mode   | VLAN | Role / Notes                    |
|-------------|------------------|---------------|------------|--------|------|---------------------------------|
| Gi1/0/1     | ESXi01           | LOM1 (vmnic0) | 1          | trunk  | 20,30,40 | ESXi01 uplink #1 (tagged)   |
| Gi1/0/2     | ESXi01           | LOM2 (vmnic1) | 2          | trunk  | 20,30,40 | ESXi01 uplink #2 (tagged)   |
| Gi1/0/3     | MS01             | LOM1          | 3          | access | TBD  | MS01 server NIC1              |
| Gi1/0/4     | MS01             | LOM2          | 4          | access | TBD  | MS01 server NIC2              |
| Gi1/0/10    | DC01             | LOM1          | 10         | access | 10   | DC01 Identity / AD            |
| Gi1/0/26    | DC01             | LOM4          | DIRECT     | access | 10   | DC01 extra NIC (future use)   |
| Gi1/0/45    | 891F Router      | GE7 (FE0/7)   | 21         | trunk  | 90   | Router Inside trunk to core   |
| Gi1/0/48    | C3560CG          | GE0/9         | 18         | trunk  | 10,20,30,40,90,99 | Core ↔ OOB/Access uplink |

All other Gi1/0/x ports: **unused / available** (to be assigned later).

---

## 2. WS‑3560CG — OOB & PAW Port Mapping

| Switch Port | Connected Device | Connected NIC | Patch Panel | Mode   | VLAN | Role / Notes                 |
|-------------|------------------|---------------|------------|--------|------|------------------------------|
| Gi0/1       | ESXi01           | iDRAC         | 13         | access | 100  | OOB mgmt ESXi01              |
| Gi0/2       | R620‑02          | iDRAC         | 14         | access | 100  | OOB mgmt R620‑02             |
| Gi0/3       | MS01             | iLO           | 15         | access | 100  | OOB mgmt MS01                |
| Gi0/8       | PAW ASUS         | NIC1          | DIRECT     | access | 99   | PAW workstation              |

Gi0/4–Gi0/7: **unused / available**.

---

## 3. ESXi01 (R620‑01) — NIC Logical Roles

| NIC      | Physical Mapping                  | Mode   | VLANs      | Role / Notes                  |
|----------|-----------------------------------|--------|------------|-------------------------------|
| vmnic0   | PP1 → Gi1/0/1 (3850)             | trunk  | 20,30,40   | ESXi uplink #1 (mgmt/VM/storage) |
| vmnic1   | PP2 → Gi1/0/2 (3850)             | trunk  | 20,30,40   | ESXi uplink #2 (redundancy)  |
| vmnic2   | (unused)                         | —      | —          | spare                         |
| vmnic3   | (unused)                         | —      | —          | spare                         |
| iDRAC    | PP13 → Gi0/1 (3560CG)            | access | 100        | OOB management                |

---

## 4. MS01 — NIC Logical Roles

| NIC   | Physical Mapping                  | Mode   | VLAN | Role / Notes                          |
|-------|-----------------------------------|--------|------|---------------------------------------|
| NIC1  | PP3 → Gi1/0/3 (3850)             | access | TBD  | Hyper‑V / infra (to be decided)       |
| NIC2  | PP4 → Gi1/0/4 (3850)             | access | TBD  | Hyper‑V / infra (redundancy/future)   |
| NIC3  | DIRECT → Home Router             | routed | —    | Out‑of‑band / internet (non‑lab)      |
| NIC4  | DIRECT → Gi1/0/26 (3850)         | access | 10   | Currently tied to DC01 LOM4 (review)  |
| iLO   | PP15 → Gi0/3 (3560CG)            | access | 100  | OOB management                        |

---

## 5. DC01 — NIC Logical Roles

| NIC   | Physical Mapping                  | Mode   | VLAN | Role / Notes                      |
|-------|-----------------------------------|--------|------|-----------------------------------|
| NIC1  | PP10 → Gi1/0/10 (3850)           | access | 10   | Identity / AD                     |
| NIC2  | DIRECT → Home Router             | routed | —    | Out‑of‑band / internet (non‑lab)  |
| NIC4  | DIRECT → Gi1/0/26 (3850)         | access | 10   | Extra NIC (future / review)       |

---

## 6. R620‑02 — NIC Logical Roles (Unassigned Hardware)

| NIC   | Physical Mapping      | Mode | VLAN | Role / Notes                 |
|-------|-----------------------|------|------|------------------------------|
| NIC1  | (unused)              | —    | —    | free                         |
| NIC2  | (unused)              | —    | —    | free                         |
| NIC3  | (unused)              | —    | —    | free                         |
| NIC4  | (unused)              | —    | —    | free                         |
| iDRAC | PP14 → Gi0/2 (3560CG) | access | 100 | OOB management only          |

---

## 7. Router Inside (Cisco 891F) — Port Mapping

| Router Port | Physical Mapping           | Mode   | VLAN | Role / Notes                     |
|-------------|----------------------------|--------|------|----------------------------------|
| FE0/7       | PP21 → Gi1/0/45 (3850)    | trunk  | 90   | Router Inside trunk to core      |
| GE0/8 (WAN) | PP14 → ISP / Home Router  | routed | —    | WAN uplink (no trunk, no VLAN)   |
| FE0/1–FE0/6 | (unused)                  | —      | —    | available                        |
| FE0/8       | (unused)                  | —      | —    | available                        |

---

## 8. PAW ASUS — Port Mapping

| NIC   | Physical Mapping          | Mode   | VLAN | Role / Notes        |
|-------|---------------------------|--------|------|---------------------|
| NIC1  | DIRECT → Gi0/8 (3560CG)  | access | 99   | PAW workstation     |

---

## 9. Patch Panel — Logical Cross‑Reference

| Patch Panel Port | Device        | NIC    | Switch Port | Mode   | VLAN | Notes                    |
|------------------|--------------|--------|------------|--------|------|--------------------------|
| 1                | ESXi01       | LOM1   | Gi1/0/1    | trunk  | 20,30,40 | ESXi uplink #1     |
| 2                | ESXi01       | LOM2   | Gi1/0/2    | trunk  | 20,30,40 | ESXi uplink #2     |
| 3                | MS01         | LOM1   | Gi1/0/3    | access | TBD  | MS01 NIC1           |
| 4                | MS01         | LOM2   | Gi1/0/4    | access | TBD  | MS01 NIC2           |
| 10               | DC01         | LOM1   | Gi1/0/10   | access | 10   | DC01 Identity       |
| 13               | ESXi01       | iDRAC  | Gi0/1      | access | 100  | OOB ESXi01          |
| 14               | R620‑02      | iDRAC  | Gi0/2      | access | 100  | OOB R620‑02         |
| 15               | MS01         | iLO    | Gi0/3      | access | 100  | OOB MS01            |
| 18               | C3560CG      | GE0/9  | Gi1/0/48   | trunk  | 10,20,30,40,90,99 | Core ↔ OOB uplink |
| 21               | 891F Router  | GE7    | Gi1/0/45   | trunk  | 90   | Router Inside trunk |

---

## 10. Notes & Follow‑Ups

- MS01 VLAN assignment (NIC1/NIC2) → **TBD** based on Hyper‑V design.  
- DC01 extra NIC (LOM4 on Gi1/0/26) → **review** if needed or disable.  
- R620‑02 remains **unassigned hardware** (no production VLANs yet).  
- Home router links (MS01 NIC3, DC01 NIC2, 891F GE0/8) are **out‑of‑band** and must be treated as non‑lab.

---

## Status

**Define Port Mapping → Completed**  
Ready to proceed to **switch configuration** and **logical validation**.
