# Routing Plan
Version: 2026‑07‑07

## 1. Purpose
Authoritative Layer‑3 routing design for the homelab.  
Defines SVI gateways, routing behavior, redistribution boundaries, and inter‑VLAN communication rules.

---

## 2. Routing Model
- **Centralized L3 routing on Cisco core switch**
- **SVI per VLAN**
- **Gateway always `.1`**
- **Static default route to firewall**
- **No dynamic routing protocols (homelab scope)**
- **DMZ routed only through firewall**
- **Storage VLAN restricted (no east‑west except ESXi)**

---

## 3. SVI Definitions

| VLAN | Name        | SVI IP         | Notes                          |
|-----:|-------------|----------------|--------------------------------|
| 10   | MGMT        | 10.10.10.1     | Core mgmt gateway              |
| 20   | VMOTION     | 10.10.20.1     | Routed but isolated            |
| 30   | STORAGE     | 10.10.30.1     | ESXi + storage only            |
| 40   | SRV-VM      | 10.10.40.1     | Server workloads               |
| 50   | INFRA-VM    | 10.10.50.1     | AD DS, PKI, ADFS, WAP          |
| 60   | PAW         | 10.10.60.1     | Admin workstations             |
| 70   | USER-LAN    | 10.10.70.1     | User endpoints                 |
| 80   | DMZ         | 10.10.80.1     | Routed only via firewall       |
| 90   | MONITORING  | 10.10.90.1     | Monitoring stack               |
| 100  | BACKUP      | 10.10.100.1    | Backup/restore                 |

---

## 4. Default Route

ip route 0.0.0.0 0.0.0.0 <FIREWALL_INSIDE_IP>
Code


Example:

ip route 0.0.0.0 0.0.0.0 10.10.50.254
Code


---

## 5. Inter‑VLAN Routing Rules (High‑Level)

### Allowed
- **PAW (60) → INFRA (50)**  
- **SRV‑VM (40) → INFRA (50)**  
- **Monitoring (90) → All zones (read‑only)**  
- **Backup (100) → INFRA (50), SRV‑VM (40)**  

### Restricted
- **User LAN (70) → INFRA (50)** (only required ports)  
- **User LAN (70) → PAW (60)** (deny)  
- **User LAN (70) → Storage (30)** (deny)  

### Forbidden (L3)
- **DMZ (80) → any internal VLAN** except via firewall  
- **Storage (30) → User LAN (70)**  
- **Storage (30) → DMZ (80)**  

---

## 6. Cisco SVI Configuration Template

```text
interface Vlan10
 description MGMT
 ip address 10.10.10.1 255.255.255.0
 no ip redirects
 no ip proxy-arp

interface Vlan20
 description VMOTION
 ip address 10.10.20.1 255.255.255.0

interface Vlan30
 description STORAGE
 ip address 10.10.30.1 255.255.255.0

interface Vlan40
 description SRV-VM
 ip address 10.10.40.1 255.255.255.0

interface Vlan50
 description INFRA-VM
 ip address 10.10.50.1 255.255.255.0

interface Vlan60
 description PAW
 ip address 10.10.60.1 255.255.255.0

interface Vlan70
 description USER-LAN
 ip address 10.10.70.1 255.255.255.0

interface Vlan80
 description DMZ
 ip address 10.10.80.1 255.255.255.0

interface Vlan90
 description MONITORING
 ip address 10.10.90.1 255.255.255.0

interface Vlan100
 description BACKUP
 ip address 10.10.100.1 255.255.255.0

7. Validation Commands

    show ip route

    show ip interface brief

    show vlan

    show run interface vlan X

    ping <gateway>

    traceroute <inter-vlan target>

