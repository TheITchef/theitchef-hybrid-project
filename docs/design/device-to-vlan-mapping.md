# Device-to-VLAN Mapping
Version: 2026‑07‑07

## 1. Purpose
Authoritative mapping of all homelab devices (physical + virtual) to their assigned VLANs.  
Ensures consistent segmentation, addressing, ACL enforcement, and switch configuration.

---

## 2. Device Categories
- Hypervisors  
- Infrastructure VMs  
- Server VMs  
- PAWs  
- User endpoints  
- DMZ servers  
- Monitoring appliances  
- Backup appliances  
- Network devices (switches, router, firewall)

---

## 3. Mapping Table

| Device / Role              | VLAN | IP Example        | Zone                |
|----------------------------|------|-------------------|----------------------|
| ESXi01 MGMT                | 10   | 10.10.10.51       | Management           |
| ESXi01 vMotion             | 20   | 10.10.20.51       | Hypervisor Svcs      |
| ESXi01 Storage             | 30   | 10.10.30.51       | Hypervisor Svcs      |
| ESXi01 VM Network          | 40   | 10.10.40.51       | Server Zone          |
| ESXi01 Infra Network       | 50   | 10.10.50.51       | Infrastructure       |
| DC01                       | 50   | 10.10.50.11       | Infrastructure       |
| DC02                       | 50   | 10.10.50.12       | Infrastructure       |
| PKI01                      | 50   | 10.10.50.13       | Infrastructure       |
| ADFS01                     | 50   | 10.10.50.14       | Infrastructure       |
| WAP01                      | 50   | 10.10.50.15       | Infrastructure       |
| PAW01                      | 60   | 10.10.60.101      | Secure Admin         |
| USERPC01                   | 70   | DHCP              | User Zone            |
| DMZ-WEB01                  | 80   | 10.10.80.11       | DMZ                  |
| MON01                      | 90   | 10.10.90.11       | Monitoring           |
| BACKUP01                   | 100  | 10.10.100.11      | Backup               |
| Cisco Core Switch          | 10   | 10.10.10.2        | Management           |
| Cisco 891F Router          | 50   | 10.10.50.254      | Infrastructure       |
| Firewall Inside Interface  | 50   | 10.10.50.253      | Infrastructure       |
| Firewall DMZ Interface     | 80   | 10.10.80.254      | DMZ                  |

---

## 4. Notes
- All mappings align with VLAN Plan, Addressing Plan, Routing Plan, ACL Plan, and Security Zones.  
- Device mapping is authoritative for switch port configuration and trunking.  
