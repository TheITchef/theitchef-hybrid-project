# Inter‑VLAN Routing Validation Procedure
## Hybrid Homelab — WS‑3850 Layer‑3 Routing Verification

---

## 1. Purpose
This procedure validates **Inter‑VLAN Routing** on the Cisco WS‑3850 L3 core switch.  
It ensures that VLANs can communicate according to the routing plan, segmentation model, and ACL enforcement strategy.

This validation is required before:
- Identity deployment  
- PKI deployment  
- ADFS/WAP federation  
- Hyper‑V and ESXi deployment  
- VM placement  
- Azure AD Connect configuration  

---

## 2. Scope
This procedure covers:
- SVI gateway reachability  
- Cross‑VLAN communication  
- Routing table validation  
- ACL enforcement  
- OOB reachability  
- PAW reachability  
- Router Inside VLAN reachability  

---

## 3. Prerequisites
- VLAN Plan completed  
- Addressing Plan completed  
- SVI interfaces configured  
- Routing Plan completed  
- ACL Plan drafted  
- WS‑3850 configured  
- PAW connected to management network  
- No ACLs blocking expected traffic  

---

## 4. Validation Tasks

### 4.1 Validate VLAN Gateway Reachability (From PAW)
Test reachability of all SVI gateways:

- `ping 192.168.10.1` — Identity VLAN  
- `ping 192.168.20.1` — ESXi Hosts VLAN  
- `ping 192.168.30.1` — VM Network VLAN  
- `ping 192.168.99.1` — PAW VLAN  
- `ping 192.168.100.1` — OOB VLAN  
- `ping 192.168.90.1` — Router Inside VLAN  

**Expected result:** All gateways reachable.

---

### 4.2 Validate Cross‑VLAN Communication
From PAW:

- Ping DC01  
- Ping ESXi01  
- Ping ESXi02  
- Ping MS01  
- Ping ADFS  
- Ping WAP  
- Ping PKI Issuing CA  

**Expected result:** All devices reachable across VLANs.

---

### 4.3 Validate Routing Table (WS‑3850)
Run:

- `show ip route 192.168.10.0`  
- `show ip route 192.168.20.0`  
- `show ip route 192.168.30.0`  
- `show ip route 192.168.99.0`  
- `show ip route 192.168.100.0`  
- `show ip route 192.168.90.0`  

**Expected result:**  
- All subnets present  
- All SVIs listed as directly connected  
- Default route pointing to Cisco 891F  

---

### 4.4 Validate ACL Behavior
Confirm:

- Identity → Compute → PKI flows allowed  
- OOB VLAN restricted  
- PAW VLAN restricted  
- WAN edge flows restricted  
- No ACL blocks expected traffic  

**Expected result:** ACLs enforce segmentation without breaking routing.

---

### 4.5 Validate OOB Management Routing
From PAW:

- Ping iLO/iDRAC interfaces  
- Ping C3560CG  
- Ping WS‑3850 management SVI  

**Expected result:** OOB reachable but isolated.

