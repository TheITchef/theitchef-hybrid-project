# Homelab Architecture Overview

## Purpose
Provide a single, high‑level architectural overview of the entire hybrid homelab environment, describing all major layers, components, and trust boundaries.  
This document acts as the master reference for identity, PKI, compute, network, and Azure integration.

## Scope
This overview covers:
- Identity architecture (AD DS, DNS, DHCP, ADFS, Azure AD Connect)
- PKI architecture (Linux Root CA, Windows Issuing CA)
- Network architecture (WS‑3850, C3560CG, Cisco 891F)
- Compute architecture (Hyper‑V, ESXi01/02)
- Azure architecture (Hybrid identity, federation)
- Automation architecture (PowerShell, Terraform)
- Trust boundaries and segmentation

## 1. Identity Architecture
From the Hybrid Homelab Project Document:
> “T330 as primary DC  
> Secondary DC VM  
> DNS + DHCP  
> Azure AD Connect  
> ADFS + WAP  
> UPN domain: theitchef.com”

### Components
- **Primary Domain Controller (T330)**  
- **Secondary Domain Controller (VM)**  
- **DNS + DHCP services**  
- **Azure AD Connect sync engine**  
- **ADFS + WAP federation pair**  
- **UPN domain:** `theitchef.com`

### Responsibilities
- Authentication & authorization  
- Directory services  
- Hybrid identity synchronization  
- Federation for modern authentication  
- DHCP relay across VLANs  
- DNS reachability across all segments

## 2. PKI Architecture
From the Hybrid Homelab Project Document:
> “Linux Root CA (offline)  
> Windows Issuing CA (online)  
> PKI VLAN isolation  
> Enterprise templates  
> Secure key storage”

### Components
- **Offline Linux Root CA**  
- **Online Windows Issuing CA**  
- **Dedicated PKI VLAN**  
- **Enterprise certificate templates**  
- **Secure key storage & issuance policies**

### Responsibilities
- Certificate lifecycle  
- Trust anchor for ADFS, ESXi, Hyper‑V, internal services  
- TLS for all internal systems  
- Secure issuance boundaries

## 3. Network Architecture
From the Hybrid Homelab Project Document:
> “WS‑3850: L3 core routing  
> C3560CG: OOB + access  
> Cisco 891F: WAN edge  
> Granular VLAN plan: Identity, PKI, ADFS, Hyper‑V host, Hyper‑V VMs, ESXi hosts, ESXi VMs, PAWs, OOB, Storage, WAN edge, Native VLAN”

### Components
- **WS‑3850** — L3 core switch  
- **C3560CG** — OOB + access  
- **Cisco 891F** — WAN edge router  
- **Patch panel + structured cabling**  
- **Granular VLAN segmentation**  
- **Inter‑VLAN routing**  
- **DHCP relay**  
- **SVI architecture**

### Responsibilities
- Routing between all VLANs  
- OOB isolation  
- WAN connectivity  
- Segmentation for identity, PKI, compute, PAWs  
- Enforcement of trust boundaries  
- ACL enforcement  
- Native VLAN control

## 4. Compute Architecture
From the Hybrid Homelab Project Document:
> “Hyper‑V host  
> ESXi01 + ESXi02  
> VM networks aligned with VLAN plan  
> Future vCenter support”

### Components
- **Hyper‑V host**  
- **ESXi01 + ESXi02**  
- **VM placement per VLAN**  
- **vCenter‑ready design**

### Responsibilities
- Virtualization platform  
- Segmented VM networks  
- Compute layer for identity, PKI, ADFS, monitoring, automation  
- Support for future vCenter deployment

## 5. Azure Architecture
From the Hybrid Homelab Project Document:
> “Azure AD Connect  
> ADFS/WAP federation  
> Terraform automation  
> Hybrid identity”

### Components
- **Azure AD tenant**  
- **Azure AD Connect**  
- **ADFS/WAP**  
- **Terraform IaC**

### Responsibilities
- Hybrid identity  
- Federation  
- Cloud integration  
- Infrastructure automation

## 6. Automation Architecture
From the Hybrid Homelab Project Document:
> “Windows PAW → PowerShell, Git  
> Linux PAW → Terraform, Root CA  
> Git repo → feature‑branch workflow  
> Obsidian Kanban → PM control”

### Components
- **Windows PAW**  
- **Linux PAW**  
- **PowerShell automation**  
- **Terraform IaC**  
- **Git feature‑branch workflow**  
- **Obsidian Kanban**

### Responsibilities
- Automated deployment  
- Infrastructure as code  
- Documentation discipline  
- Predictable change control

## 7. Trust Boundaries & Security Zones
Derived from VLAN segmentation + PKI isolation:
- Identity zone  
- PKI zone  
- ADFS/WAP zone  
- Hyper‑V host zone  
- Hyper‑V VM zone  
- ESXi host zone  
- ESXi VM zone  
- PAW zone  
- OOB zone  
- Storage zone  
- WAN edge zone  
- Native VLAN

Each zone has:
- Defined ACLs  
- Routing rules  
- Allowed flows  
- Security expectations  

## 8. High‑Level Diagram (ASCII placeholder)

+----------------------+
|      Azure AD        |
+----------+-----------+
|
ADFS / WAP
|
+--------------------------+--------------------------+
|                     Identity VLAN                   |
|  DC01 (T330)     DC02 (VM)     DNS/DHCP             |
+--------------------------+--------------------------+
|
Core WS‑3850
|
-------------------------------------------------
|                 |                 |           |
PKI VLAN        Compute VLAN       PAW VLAN     OOB VLAN
Root CA / Issuer   Hyper‑V / ESXi     Windows PAW  C3560CG
|                 |                 |           |
Cisco 891F (WAN Edge)
Code


## 9. References
- Hybrid Homelab Project Document  
- README.md  
- Architecture folder documents  

## 10. Monitoring Architecture
From the Hybrid Homelab Project Document:
> “Monitoring Architecture”  


### Components
- Central monitoring VM
- Syslog ingestion
- SNMP polling
- Certificate-based secure telemetry
- Azure monitoring integration (future)

### Responsibilities
- Health visibility across identity, PKI, compute, and network
- Alerting for critical events
- Log retention and correlation
- PKI certificate expiry monitoring
