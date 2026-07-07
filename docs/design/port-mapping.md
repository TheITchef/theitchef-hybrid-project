# Port Mapping
Version: 2026‑07‑07

## 1. Purpose
Authoritative mapping of all switch ports to physical devices, VLANs, and trunk/access modes.  
Ensures consistent cabling, configuration, and troubleshooting.

---

## 2. Port Naming Standard
- `Gi1/0/X` → Cisco 3850  
- `Gi0/X` → Cisco 3560CG  
- Description format:

<DEVICE> | <ROLE> | <VLAN or TRUNK>
Code


Example:

ESXi01 | MGMT | VLAN10
Code


---

## 3. Core Switch (Cisco 3850) Port Mapping

| Port     | Device / Role              | Mode   | VLANs / Trunk Set                     |
|----------|-----------------------------|--------|----------------------------------------|
| Gi1/0/1  | ESXi01 MGMT                 | trunk  | 10,20,30,40,50                         |
| Gi1/0/2  | ESXi01 Uplink 2             | trunk  | 10,20,30,40,50                         |
| Gi1/0/3  | Firewall Inside             | trunk  | 10,40,50,80                            |
| Gi1/0/4  | Firewall DMZ                | trunk  | 80                                     |
| Gi1/0/5  | DC01                        | access | 50                                     |
| Gi1/0/6  | DC02                        | access | 50                                     |
| Gi1/0/7  | PKI01                       | access | 50                                     |
| Gi1/0/8  | ADFS01                      | access | 50                                     |
| Gi1/0/9  | WAP01                       | access | 50                                     |
| Gi1/0/10 | PAW01                       | access | 60                                     |
| Gi1/0/11 | USERPC01                    | access | 70                                     |
| Gi1/0/12 | DMZ-WEB01                   | access | 80                                     |
| Gi1/0/13 | MON01                       | access | 90                                     |
| Gi1/0/14 | BACKUP01                    | access | 100                                    |

---

## 4. Access Switch (Cisco 3560CG) Port Mapping

| Port   | Device / Role | Mode   | VLAN |
|--------|----------------|--------|------|
| Gi0/1  | USERPC02       | access | 70   |
| Gi0/2  | USERPC03       | access | 70   |
| Gi0/3  | PAW02          | access | 60   |
| Gi0/4  | PAW03          | access | 60   |

---

## 5. ESXi vSwitch → Physical NIC Mapping

| ESXi vmnic | Connected Port | VLANs / Purpose |
|------------|----------------|------------------|
| vmnic0     | Gi1/0/1        | MGMT (10)        |
| vmnic1     | Gi1/0/2        | vMotion (20)     |
| vmnic2     | Gi1/0/1        | Storage (30)     |
| vmnic3     | Gi1/0/2        | VM Networks (40,50) |

---

## 6. Notes
- All mappings align with VLAN, trunking, addressing, routing, ACL, and zone definitions.  
- This document is authoritative for switch configuration and cabling verification.  