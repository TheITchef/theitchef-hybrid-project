# PKI Architecture
## Hybrid Homelab — Two‑Tier Public Key Infrastructure

---

## 1. Overview
This document defines the architecture of the **two‑tier PKI** used in the hybrid homelab environment.  
The PKI provides certificate services for identity, federation, secure communication, device trust, and workload authentication across on‑premises and cloud‑integrated systems.

The PKI follows enterprise best practices:
- Offline Root CA (Linux)
- Online Issuing CA (Windows Server)
- Segmented PKI VLAN
- CRL/AIA publication
- Template‑based certificate issuance
- Integration with AD DS, ADFS, WAP, ESXi, Hyper‑V, and Azure AD Connect

---

## 2. Scope
This architecture covers:
- PKI tiering model  
- Root CA design  
- Issuing CA design  
- Certificate templates  
- CRL/AIA distribution  
- PKI network segmentation  
- Security controls  
- Integration points  
- Operational lifecycle  

---

## 3. PKI Tiering Model

### 3.1 Tier 0 — Offline Root CA
- Linux‑based CA  
- Physically offline  
- Used only to sign Issuing CA certificate  
- Stored in secure offline media  
- No network connectivity  
- Long‑term validity (10–20 years)  
- Private key protected by encrypted removable storage  

### 3.2 Tier 1 — Online Issuing CA
- Windows Server  
- Domain‑joined  
- Issues certificates to:
  - Domain controllers  
  - Servers (ADFS, WAP, Hyper‑V, ESXi)  
  - Workstations  
  - Devices  
  - Services  
- Shorter validity periods (1–5 years)  
- CRL/AIA published to internal web endpoints  
- Managed via PAW  

---

## 4. PKI Network Segmentation

### 4.1 PKI VLAN
- Dedicated VLAN for Issuing