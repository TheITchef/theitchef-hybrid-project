# Backup Strategy
## Hybrid Homelab — Enterprise Backup & Recovery Architecture

---

## 1. Overview
This document defines the **Backup Strategy Architecture** for the hybrid homelab environment.  
It ensures data protection, service continuity, and recoverability across identity, compute, PKI, network, and federation components.

The strategy follows enterprise principles:
- Multi‑layer backup model  
- Immutable backup copies  
- Offline storage  
- Application‑aware backups  
- PKI‑specific backup handling  
- Recovery testing and validation  

---

## 2. Scope
This architecture covers:
- Backup tiers  
- Backup targets  
- Backup frequency  
- PKI backup requirements  
- AD DS backup requirements  
- Hypervisor backup strategy  
- VM‑level backup strategy  
- Offsite/offline backup handling  
- Recovery workflows  
- Monitoring and validation  

---

## 3. Backup Architecture Model

### 3.1 Tier 0 — Critical Identity & PKI
Components:
- Offline Root CA  
- Online Issuing CA  
- AD DS Domain Controllers  
- ADFS  
- WAP  

Backup requirements:
- System state backups  
- PKI private key backups  
- CA database backups  
- Token signing/decrypting certificates  
- Federation configuration  

### 3.2 Tier 1 — Compute & Virtualization
Components:
- Hyper‑V hosts  
- ESXi hosts  
- VM configurations  
- VM disks (VHDX / VMDK)  

Backup requirements:
- Host configuration export  
- VM‑level backups  
- Application‑aware backups for AD DS, ADFS, PKI  

### 3.3 Tier 2 — Network & Infrastructure
Components:
- Cisco switch configurations  
- VLAN plans  
- Routing tables  
- ACLs  
- OOB management configuration  

Backup requirements:
- Configuration export  
- Secure storage in Git repository  
- Offline copy  

---

## 4. Backup Frequency

### 4.1 Daily
- VM‑level backups  
- AD DS system state  
- ADFS configuration  
- WAP configuration  
- PKI Issuing CA database  

### 4.2 Weekly
- Full VM backups  
- Hyper‑V host configuration  
- ESXi host configuration  
- Cisco switch configuration export  

### 4.3 Monthly
- Offline Root CA CRL update  
- Root CA backup (manual)  
- Full infrastructure snapshot  

### 4.4 On‑Demand
- Before major changes  
- Before PKI operations  
- Before identity changes  
- Before network re‑segmentation  

---

## 5. Backup Storage Strategy

### 5.1 Primary Backup Repository
- Hosted on MS01  
- Veeam Community Edition  
- Application‑aware backups  
- Daily retention  

### 5.2 Secondary Backup Repository
- External USB SSD  
- Stored offline  
- Weekly sync  
- Used for disaster recovery  

### 5.3 Immutable Backup Copy
- Write‑once storage  
- Monthly copy  
- Stored offsite  

---

## 6. PKI‑Specific Backup Requirements

### 6.1 Root CA
- Offline  
- Private key backup  
- CA certificate  
- CRL  
- Stored on encrypted removable media  
- Stored in fireproof safe  

### 6.2 Issuing CA
- CA database  
- Private key  
- Certificate templates  
- CRL/AIA configuration  
- System state backup  

---

## 7. AD DS Backup Requirements
- System state backup  
- NTDS.dit  
- SYSVOL  
- DNS zones  
- AD‑integrated PKI objects  
- Authoritative/non‑authoritative restore procedures  

---

## 8. Hypervisor Backup Requirements

### 8.1 Hyper‑V
- Host configuration export  
- VM configuration export  
- VHDX backups  
- Application‑aware backups  

### 8.2 ESXi
- Host profile export  
- VM configuration export  
- VMDK backups  
- vCenter configuration (future)  

---

## 9. Network Backup Requirements
- Cisco switch configuration export  
- VLAN definitions  
- ACL tables  
- Routing plans  
- OOB management configuration  

Stored in:
- Git repository  
- Offline backup media  

---

## 10. Recovery Workflows

### 10.1 Identity Recovery
- Restore AD DS system state  
- Restore PKI Issuing CA  
- Restore ADFS  
- Restore WAP  
- Validate federation  

### 10.2 Compute Recovery
- Restore VM from backup  
- Restore hypervisor configuration  
- Validate network connectivity  

### 10.3 PKI Recovery
- Restore CA database  
- Restore private key  
- Re‑publish CRL/AIA  
- Validate certificate issuance  

### 10.4 Network Recovery
- Restore switch configuration  
- Validate VLANs  
- Validate routing  
- Validate ACLs  

---

## 11. Monitoring & Validation
- Daily backup job monitoring  
- Weekly restore testing  
- Monthly DR simulation  
- Quarterly PKI recovery test  
- Backup integrity checks  
- Immutable copy verification  

---

## 12. Deliverables
- Backup Strategy Document  
- Backup configuration (Veeam)  
- Backup repository  
- Offline backup media  
- Immutable backup copy  
- Recovery workflows  
- DR test results  

---

## 13. Acceptance Criteria
- All critical systems backed up  
- PKI backups validated  
- AD DS restore tested  
- VM restore tested  
- Network restore validated  
- Documentation complete  
