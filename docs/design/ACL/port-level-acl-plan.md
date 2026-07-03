# Port‑Level ACL Plan

## Purpose
Define exact TCP/UDP ports allowed between VLANs to enforce Tier‑0 security while maintaining required functionality (AD, DNS, ESXi, VM management, OOB, Router Inside).

## Tier‑0 VLANs
- VLAN 10 — Identity
- VLAN 20 — ESXi Hosts
- VLAN 90 — Router Inside
- VLAN 99 — PAWs
- VLAN 100 — OOB Management

## Tier‑1 VLAN
- VLAN 30 — VM / Infra

---

# VLAN 10 — Identity (AD DS + DNS)

## Allowed: VLAN 30 → VLAN 10 (AD/DNS)
- TCP/UDP 53 — DNS  
- TCP/UDP 88 — Kerberos  
- TCP 135 — RPC  
- TCP/UDP 389 — LDAP  
- TCP 445 — SMB  
- TCP 636 — LDAPS  
- TCP 3268/3269 — Global Catalog  
- UDP 123 — NTP  

## Allowed: VLAN 99 → VLAN 10 (PAWs)
- All ports above  
- TCP 3389 — RDP  
- TCP 5985/5986 — WinRM  
- TCP 443 — ADFS / admin portals  

## Deny
- VLAN 20 → VLAN 10 (except DNS/AD if ESXi uses AD)  
- VLAN 90 → VLAN 10  
- VLAN 100 → VLAN 10  

---

# VLAN 20 — ESXi Hosts

## Allowed: VLAN 99 → VLAN 20 (PAWs)
- TCP 443 — ESXi/vCenter  
- TCP 902 — ESXi mgmt  
- TCP 22 — SSH  

## Allowed: VLAN 10 → VLAN 20 (Identity)
- TCP/UDP 53 — DNS  
- TCP 88, 389, 445 — AD integration  

## Deny
- VLAN 30 → VLAN 20  
- VLAN 90 → VLAN 20  
- VLAN 100 → VLAN 20  

---

# VLAN 30 — VM / Infra

## Allowed: VLAN 30 → VLAN 10 (AD/DNS)
- Same AD/DNS ports as Identity section

## Deny
- VLAN 30 → VLAN 20  
- VLAN 30 → VLAN 90  
- VLAN 30 → VLAN 100  

---

# VLAN 99 — PAWs (Tier‑0 Admin)

## Allowed: VLAN 99 → All VLANs
- Identity: AD/DNS + RDP + WinRM + admin web  
- ESXi: 443, 902, 22  
- VM workloads: RDP/WinRM/SSH  
- Router Inside: SSH/HTTPS  
- OOB: iDRAC/iLO/SSH/HTTPS  

## Deny
- None — PAWs are Tier‑0

---

# VLAN 100 — OOB Management

## Allowed
- VLAN 99 → VLAN 100  
  - TCP 443 — iDRAC/iLO  
  - TCP 22 — SSH  
  - Vendor mgmt ports  

## Deny
- All other VLANs → VLAN 100  

---

# VLAN 90 — Router Inside

## Allowed
- VLAN 99 → VLAN 90  
  - TCP 22 — SSH  
  - TCP 443 — HTTPS  
  - ICMP — diagnostics  

## Deny
- All other VLANs → VLAN 90  

---

# ACL Binding Model (WS‑3850)

ACLs applied inbound on SVIs:

| VLAN | ACL Name |
|------|----------|
| 10 | ACL‑IN‑VLAN10 |
| 20 | ACL‑IN‑VLAN20 |
| 30 | ACL‑IN‑VLAN30 |
| 99 | ACL‑IN‑VLAN99 |
| 100 | ACL‑IN‑VLAN100 |

---

## Status
Port‑Level ACL Plan generated — ready for ACL table generation or Cisco configuration output.
