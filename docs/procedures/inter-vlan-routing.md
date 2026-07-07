# Inter-VLAN Routing Procedure
Version: 2026‑07‑07

## 1. Purpose
Step-by-step procedure for enabling, validating, and troubleshooting inter‑VLAN routing on the Cisco core switch.  
Aligns with VLAN Plan, Addressing Plan, Routing Plan, ACL Plan, and Security Zones.

---

## 2. Prerequisites
- VLANs created according to `vlan-plan.md`
- SVI gateways defined according to `routing-plan.md`
- ACLs applied according to `acl-plan.md`
- Trunking configured according to `trunking-strategy.md`
- Port mapping validated according to `port-mapping.md`

---

## 3. Enable IP Routing

conf t
ip routing
end
Code


Verification:

show ip route
Code


---

## 4. Create SVIs for Each VLAN

Example:

interface Vlan50
description INFRA-VM
ip address 10.10.50.1 255.255.255.0
no ip redirects
no ip proxy-arp
ip access-group ACL_INFRA in
Code


Repeat for all VLANs defined in the routing plan.

Verification:

show ip interface brief | include Vlan
Code


---

## 5. Configure Default Route

ip route 0.0.0.0 0.0.0.0 10.10.50.254
Code


Verification:

show ip route static
Code


---

## 6. Validate Inter‑VLAN Connectivity

### Step 1 — Ping gateways

ping 10.10.10.1
ping 10.10.20.1
ping 10.10.30.1
...
Code


### Step 2 — Ping between VLANs (allowed flows only)

Examples:

ping 10.10.50.11   ! DC01
ping 10.10.40.51   ! ESXi VM network
ping 10.10.60.101  ! PAW01
Code


### Step 3 — Test blocked flows (ACL enforcement)

ping 10.10.60.101 source 10.10.70.50   ! User → PAW (should fail)
ping 10.10.30.51 source 10.10.70.50    ! User → Storage (should fail)
Code


---

## 7. Troubleshooting

### Check SVI status

show run interface vlan X
show ip interface vlan X
Code


### Check ACL hits

show access-lists ACL_<NAME>
Code


### Check trunk status

show interfaces trunk
Code


### Check MAC learning

show mac address-table vlan X
Code


### Check ARP

show ip arp vlan X
Code


---

## 8. Notes
- All routing behavior must align with ACL Plan and Security Zones.  
- DMZ routing must always pass through the firewall.  
- Storage VLAN must remain isolated except for ESXi and backup flows.  