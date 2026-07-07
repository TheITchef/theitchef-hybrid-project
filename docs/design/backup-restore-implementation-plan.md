# Backup & Restore Implementation Plan
Version: 2026‑07‑07  
Author: Ioannis Mintzivyris

## 1. Purpose
Define the implementation plan for deploying, validating, and operationalizing the backup and restore strategy described in `backup-strategy.md`.  
This plan covers backup repository setup, job configuration, PKI‑specific handling, VM‑level backups, network device configuration exports, and restore validation.

---

## 2. Scope
This implementation plan applies to:

- Veeam Backup Repository (MS01)
- External USB SSD (offline weekly copy)
- Immutable monthly backup media
- Hyper‑V hosts
- ESXi01 hypervisor
- Infrastructure VMs (DC01, DC02, PKI01, ADFS01, WAP01)
- Server VMs
- Cisco WS‑3850 core switch
- Cisco 891F router
- Firewall (Inside + DMZ)
- PKI Root CA (offline)
- PKI Issuing CA

---

## 3. Implementation Phases

### **Phase 1 — Backup Infrastructure Preparation**
1. Deploy Veeam Community Edition on MS01  
2. Configure backup repository:
   - Primary: MS01 local storage  
   - Secondary: External USB SSD  
   - Monthly immutable media  
3. Validate storage health  
   (Storage inventory confirms RAID0 1TB logical drive is operational)

### **Phase 2 — VM Backup Job Configuration**
Create Veeam jobs:

#### **Daily Incremental**
- DC01  
- DC02  
- PKI01  
- ADFS01  
- WAP01  
- Server VMs  
- ESXi01 management VM (if applicable)

#### **Weekly Full**
- All VMs  
- Hyper‑V host configuration export  
- ESXi01 host configuration export  

#### **Monthly Immutable Copy**
- Export full backups to write‑once media  
- Store offsite

### **Phase 3 — PKI Backup Handling**
#### **Root CA (Offline)**
- Export private key to encrypted removable media  
- Export CA certificate  
- Export CRL  
- Store in fireproof safe  
- Document recovery steps

#### **Issuing CA**
- Backup CA database  
- Backup private key  
- Backup certificate templates  
- Backup system state  
- Validate restore using test VM

### **Phase 4 — Identity Backup**
#### **AD DS**
- Daily system state backup  
- Backup NTDS.dit  
- Backup SYSVOL  
- Backup DNS zones  
- Validate authoritative + non‑authoritative restore procedures

### **Phase 5 — Network Device Configuration Backups**
#### **WS‑3850 Core Switch**
Export configuration weekly:

copy running-config tftp://10.10.100.11/ws3850.cfg
Code


#### **Cisco 891F Router**

copy running-config tftp://10.10.100.11/router-891f.cfg
Code


#### **Firewall**
Export inside + DMZ configuration:

set system config-export tftp://10.10.100.11/firewall.cfg
Code


### **Phase 6 — ESXi & Hyper‑V Backup Integration**
#### **ESXi01**
- Export host profile  
- Export VM configurations  
- Backup VMDKs via Veeam  
- Validate restore on test datastore

#### **Hyper‑V**
- Export host configuration  
- Backup VHDX files  
- Validate VM restore

### **Phase 7 — Backup Copy Jobs**
#### **Weekly Offline Copy**
- Sync backups to external USB SSD  
- Disconnect and store offline

#### **Monthly Immutable Copy**
- Write‑once media  
- Store offsite

### **Phase 8 — Restore Validation**
Perform quarterly restore tests:

#### **Identity**
- Restore DC01 system state  
- Validate AD replication  
- Validate PKI Issuing CA restore  
- Validate ADFS/WAP restore

#### **Compute**
- Restore VM from backup  
- Validate network connectivity  
- Validate application functionality

#### **Network**
- Restore switch configuration  
- Validate VLANs, ACLs, routing  
- Restore router configuration  
- Validate firewall rules

---

## 4. Operational Checklist

### **Daily**
- Verify backup job success  
- Check Veeam logs  
- Check repository free space  

### **Weekly**
- Perform offline backup copy  
- Validate configuration exports  

### **Monthly**
- Create immutable backup  
- Perform DR simulation  

### **Quarterly**
- Full restore test  
- PKI recovery test  
- Backup integrity verification  

---

## 5. Notes
- PKI backups require strict handling and offline storage  
- Immutable backups protect against corruption and ransomware  
- Restore validation is mandatory for DR readiness  
- All backup flows must align with ACL Plan and Security Zones  