# Switch Configuration Template
Version: 2026‑07‑07

## 1. Purpose
Authoritative baseline configuration template for Cisco switches in the homelab.  
Ensures consistency across core and access switches.

---

## 2. Global Configuration

service timestamps debug datetime msec
service timestamps log datetime msec
no ip domain-lookup
ip domain-name lab.theitchef.com

logging buffered 64000
logging host 10.10.90.11

ntp server 10.10.50.11
crypto key generate rsa modulus 2048

banner motd ^C
UNAUTHORIZED ACCESS PROHIBITED
^C
Code


---

## 3. VLAN Definitions

vlan 10
name MGMT
vlan 20
name VMOTION
vlan 30
name STORAGE
vlan 40
name SRV-VM
vlan 50
name INFRA-VM
vlan 60
name PAW
vlan 70
name USER-LAN
vlan 80
name DMZ
vlan 90
name MONITORING
vlan 100
name BACKUP
Code


---

## 4. SVI Template

interface VlanXX
description <NAME>
ip address <GATEWAY> 255.255.255.0
no ip redirects
no ip proxy-arp
ip access-group ACL_<NAME> in
Code


---

## 5. Trunk Template

interface GiX/X
description <DEVICE> | TRUNK
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60,70,80,90,100
switchport trunk native vlan none
switchport nonegotiate
spanning-tree portfast trunk
Code


---

## 6. Access Template

interface GiX/X
description <DEVICE> | VLAN<VID>
switchport mode access
switchport access vlan <VID>
spanning-tree portfast
Code


---

## 7. Management Interface

interface Vlan10
description MGMT
ip address 10.10.10.2 255.255.255.0
Code


---

## 8. Default Route

ip route 0.0.0.0 0.0.0.0 10.10.50.254
Code


---

## 9. ACL Attachment Example

ip access-list extended ACL_INFRA
permit tcp 10.10.60.0 0.0.0.255 10.10.50.0 0.0.0.255 eq 3389
deny ip any any log

interface Vlan50
ip access-group ACL_INFRA in
Code


---

## 10. Notes
- Template aligns with VLAN, trunking, addressing, routing, ACL, zones, and port mapping documents.  
- This is the authoritative baseline for all switch deployments.