# VLAN Plan
Version: 2026‑07‑07

## 1. Purpose
Authoritative VLAN structure for the homelab.  
Foundation for trunking, addressing, routing, ACLs, segmentation, port mapping, switch templates, PKI, monitoring, DR.

---

## 2. VLAN Table

| VLAN ID | Name                     | Purpose                               | Zone                | Trust |
|--------:|--------------------------|----------------------------------------|----------------------|-------|
| 10      | MGMT                     | ESXi mgmt, switch mgmt, OOB mgmt       | Management Zone      | High  |
| 20      | VMOTION                  | ESXi vMotion network                   | Hypervisor Services  | High  |
| 30      | STORAGE                  | iSCSI/NFS storage traffic              | Storage Zone         | High  |
| 40      | SRV-VM                   | Server workloads                       | Server Zone          | Medium|
| 50      | INFRA-VM                 | AD DS, PKI, ADFS, WAP, infra VMs       | Infrastructure Zone  | High  |
| 60      | PAW                      | Privileged Access Workstations         | Secure Admin Zone    | High  |
| 70      | USER-LAN                 | User endpoints                         | User Zone            | Low   |
| 80      | DMZ                      | Public‑facing services                 | DMZ Zone             | Low   |
| 90      | MONITORING               | Monitoring stack                       | Infra Zone           | High  |
| 100     | BACKUP                   | Backup/restore network                 | Infra Zone           | High  |

---

## 3. Routing Requirements
- Routed VLANs: 10, 20, 30, 40, 50, 60, 70, 90, 100  
- Non‑routed: 80 (DMZ isolated except via firewall)

---

## 4. ACL Requirements (High‑Level)
- PAW (60) → Infra (50) only  
- User LAN (70) → Infra (50) restricted  
- DMZ (80) → Infra (50) via firewall only  
- Storage (30) → ESXi only  
- Monitoring (90) → All zones (read‑only)

---

## 5. Trunking Requirements
- All uplinks carry: 10,20,30,40,50,60,70,80,90,100  
- DMZ (80) only on firewall‑connected trunks  
- Storage (30) only on ESXi + storage switches

---

## 6. Device Membership (High‑Level)
- ESXi01 → 10,20,30,40,50  
- AD DS / PKI / ADFS / WAP → 50  
- PAW → 60  
- User endpoints → 70  
- DMZ servers → 80  
- Monitoring stack → 90  
- Backup appliances → 100

---

## 7. Notes
- VLAN numbering deterministic and scalable  
- No overlaps  
- Supports all Priority tasks  
