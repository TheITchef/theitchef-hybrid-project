# Security Zones & Trust Boundaries
Version: 2026‑07‑07

## 1. Purpose
Define logical security zones and trust boundaries for the homelab network.  
This document is the reference for segmentation, ACLs, firewall rules, and privileged access design.

---

## 2. Security Zones

| Zone              | VLANs                 | Trust Level | Description                               |
|-------------------|-----------------------|------------|-------------------------------------------|
| Management        | 10                    | High       | Switch, ESXi, OOB management              |
| Hypervisor Svcs   | 20, 30                | High       | vMotion, storage                          |
| Infrastructure    | 50, 90, 100           | High       | AD DS, PKI, ADFS, WAP, monitoring, backup |
| Server Zone       | 40                    | Medium     | Application and service VMs               |
| Secure Admin      | 60                    | High       | PAW / admin workstations                  |
| User Zone         | 70                    | Low        | User endpoints                            |
| DMZ               | 80                    | Low        | Public‑facing services                     |

---

## 3. Trust Boundaries

- **User Zone ↔ Infrastructure Zone**  
  - Boundary enforced by ACLs and firewall  
  - Only required ports (HTTPS, specific app ports) allowed.

- **DMZ ↔ Internal Zones**  
  - Hard boundary at firewall.  
  - No direct L3 from DMZ to internal VLANs; all flows via firewall.

- **Secure Admin (PAW) ↔ Infrastructure**  
  - High‑trust path for admin operations.  
  - PAW allowed to manage Infra and Server zones; blocked from User zone.

- **Storage ↔ All Other Zones**  
  - Storage only reachable from ESXi and backup services.  
  - No User/DMZ/PAW direct access.

- **Monitoring ↔ All Zones**  
  - Read‑only visibility across all zones.  
  - No user‑initiated traffic from monitored zones back to Monitoring.

---

## 4. Design Principles

- **Least privilege** between zones.  
- **No direct DMZ → Internal** without firewall inspection.  
- **Admin actions only from PAW, never from User Zone.**  
- **Storage and Management zones treated as critical assets.**

---

## 5. Implementation References

- VLAN Plan → `docs/design/vlan-plan.md`  
- Addressing Plan → `docs/design/addressing-plan.md`  
- Routing Plan → `docs/design/routing-plan.md`  
- ACL Plan → `docs/design/acl-plan.md`  

