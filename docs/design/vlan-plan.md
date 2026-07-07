# ACL Plan
Version: 2026‑07‑07

## 1. Purpose
Define all Layer‑3 access control rules governing inter‑VLAN communication.  
This document enforces segmentation, trust boundaries, and least‑privilege routing.

---

## 2. ACL Model
- **Centralized ACLs on core L3 switch**
- **Inbound ACLs applied per SVI**
- **Explicit deny at end of each ACL**
- **DMZ traffic forced through firewall**
- **Storage VLAN protected (ESXi only)**
- **PAW → Infra allowed**
- **User LAN → Infra restricted**
- **Monitoring → read‑only access to all zones**

---

## 3. ACL Structure
Each VLAN gets its own ACL:

ip access-list extended ACL_<VLAN_NAME>
<rules>
deny ip any any log
Code


Applied inbound:

interface VlanXX
ip access-group ACL_<VLAN_NAME> in
Code


---

## 4. ACL Definitions

### **ACL_INFRA (VLAN 50)**  
Allow essential inbound traffic:

ip access-list extended ACL_INFRA
permit tcp 10.10.60.0 0.0.0.255 10.10.50.0 0.0.0.255 eq 3389      ! PAW → Infra RDP
permit tcp 10.10.40.0 0.0.0.255 10.10.50.0 0.0.0.255 eq 445       ! Servers → Infra SMB
permit tcp 10.10.40.0 0.0.0.255 10.10.50.0 0.0.0.255 eq 389       ! Servers → Infra LDAP
permit tcp 10.10.90.0 0.0.0.255 10.10.50.0 0.0.0.255 any          ! Monitoring → Infra
deny ip 10.10.70.0 0.0.0.255 10.10.50.0 0.0.0.255                 ! User LAN → Infra (default deny)
deny ip any any log
Code


---

### **ACL_PAW (VLAN 60)**  
PAW is high‑trust, outbound allowed only to Infra:

ip access-list extended ACL_PAW
permit ip 10.10.60.0 0.0.0.255 10.10.50.0 0.0.0.255
deny ip any any log
Code


---

### **ACL_USER (VLAN 70)**  
User LAN is low‑trust:

ip access-list extended ACL_USER
permit tcp 10.10.70.0 0.0.0.255 10.10.50.0 0.0.0.255 eq 443       ! User → Infra HTTPS only
deny ip 10.10.70.0 0.0.0.255 10.10.60.0 0.0.0.255                 ! User → PAW
deny ip 10.10.70.0 0.0.0.255 10.10.30.0 0.0.0.255                 ! User → Storage
deny ip any any log
Code


---

### **ACL_STORAGE (VLAN 30)**  
Storage is extremely restricted:

ip access-list extended ACL_STORAGE
permit ip 10.10.30.0 0.0.0.255 host 10.10.40.51                   ! ESXi host only
deny ip any any log
Code


---

### **ACL_DMZ (VLAN 80)**  
DMZ cannot reach internal networks directly:

ip access-list extended ACL_DMZ
deny ip 10.10.80.0 0.0.0.255 10.10.0.0 0.0.255.255                ! DMZ → Internal
permit ip 10.10.80.0 0.0.0.255 <FIREWALL_IP>                      ! DMZ → Firewall only
deny ip any any log
Code


---

### **ACL_MONITORING (VLAN 90)**  
Monitoring has read‑only access:

ip access-list extended ACL_MONITORING
permit ip 10.10.90.0 0.0.0.255 any
deny ip any any log
Code


---

## 5. Validation Commands
- `show ip access-lists`
- `show ip interface`
- `show run interface vlan X`
- `show access-lists ACL_<NAME>`
- Test flows with `ping` and `telnet <ip> <port>`

---

## 6. Notes
- ACLs follow least‑privilege  
- DMZ isolation enforced  
- Storage protected  
- PAW privileged  
- User LAN restricted  
- Monitoring allowed read‑only visibility  