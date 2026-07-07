# Addressing Plan
Version: 2026‑07‑07

## 1. Purpose
Authoritative IP addressing scheme for all VLANs.  
Foundation for routing, ACLs, segmentation, port mapping, switch templates, monitoring, DR, PKI, and ESXi design.

---

## 2. Addressing Model
- IPv4 only (homelab scope)
- /24 per VLAN (simple, deterministic, scalable)
- Gateway always `.1`
- Reserved ranges:
  - `.1` → SVI gateway
  - `.2-.10` → core infra (routers, firewalls)
  - `.11-.50` → servers
  - `.51-.100` → hypervisors
  - `.101-.150` → appliances
  - `.151-.200` → endpoints
  - `.201-.254` → future use

---

## 3. VLAN Address Allocation

| VLAN | Name        | Subnet            | Gateway     | Notes                          |
|-----:|-------------|-------------------|-------------|--------------------------------|
| 10   | MGMT        | 10.10.10.0/24     | 10.10.10.1  | ESXi mgmt, switch mgmt, OOB    |
| 20   | VMOTION     | 10.10.20.0/24     | 10.10.20.1  | ESXi vMotion only              |
| 30   | STORAGE     | 10.10.30.0/24     | 10.10.30.1  | iSCSI/NFS storage              |
| 40   | SRV-VM      | 10.10.40.0/24     | 10.10.40.1  | Server workloads               |
| 50   | INFRA-VM    | 10.10.50.0/24     | 10.10.50.1  | AD DS, PKI, ADFS, WAP, infra   |
| 60   | PAW         | 10.10.60.0/24     | 10.10.60.1  | Privileged Access Workstations |
| 70   | USER-LAN    | 10.10.70.0/24     | 10.10.70.1  | User endpoints                 |
| 80   | DMZ         | 10.10.80.0/24     | 10.10.80.1  | Public-facing services         |
| 90   | MONITORING  | 10.10.90.0/24     | 10.10.90.1  | Monitoring stack               |
| 100  | BACKUP      | 10.10.100.0/24    | 10.10.100.1 | Backup/restore network         |

---

## 4. ESXi Host Addressing (Example)
- ESXi01 MGMT → 10.10.10.51  
- ESXi01 vMotion → 10.10.20.51  
- ESXi01 Storage → 10.10.30.51  
- ESXi01 VM Network → 10.10.40.51  
- ESXi01 Infra → 10.10.50.51  

---

## 5. Infra VM Addressing (Example)
- DC01 → 10.10.50.11  
- DC02 → 10.10.50.12  
- PKI01 → 10.10.50.13  
- ADFS01 → 10.10.50.14  
- WAP01 → 10.10.50.15  

---

## 6. Notes
- Deterministic numbering  
- No overlaps  
- Supports all downstream tasks  
- Aligns with VLAN + trunking strategy  
