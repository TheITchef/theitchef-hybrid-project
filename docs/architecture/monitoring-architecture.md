# Monitoring Architecture
## Hybrid Homelab — Observability & Health Monitoring Design

---

## 1. Overview
This document defines the **Monitoring Architecture** for the hybrid homelab environment.  
It ensures visibility, health tracking, alerting, and operational awareness across identity, compute, PKI, network, and federation components.

Monitoring in this environment follows enterprise principles:
- Multi‑layer observability  
- Event‑driven alerting  
- Log centralization  
- Health dashboards  
- Backup + DR validation  
- PKI + identity monitoring  
- Hypervisor + VM monitoring  
- Network telemetry  

---

## 2. Scope
This architecture covers:
- Monitoring layers  
- Monitoring tools  
- Identity monitoring  
- PKI monitoring  
- ADFS/WAP monitoring  
- Hyper‑V + ESXi monitoring  
- Cisco network monitoring  
- Backup + DR monitoring  
- Log aggregation  
- Alerting strategy  

---

## 3. Monitoring Layers

### 3.1 Layer 0 — Hardware Health
- Server temperature  
- Fan status  
- Power supply health  
- RAID status  
- Disk SMART data  
- iDRAC/iLO telemetry  

### 3.2 Layer 1 — Hypervisor Health
- Hyper‑V host metrics  
- ESXi host metrics  
- VM CPU/RAM usage  
- VM disk latency  
- VM network throughput  

### 3.3 Layer 2 — Identity & PKI Health
- AD DS replication  
- DNS health  
- DHCP health  
- PKI Issuing CA status  
- CRL/AIA publication  
- Certificate issuance failures  

### 3.4 Layer 3 — Federation Health
- ADFS token issuance  
- ADFS certificate expiration  
- WAP proxy trust  
- Azure AD Connect sync status  

### 3.5 Layer 4 — Network Health
- Cisco WS‑3850 routing  
- Cisco C3560CG OOB  
- Cisco 891F WAN edge  
- VLAN reachability  
- Inter‑VLAN routing  
- ACL enforcement  

### 3.6 Layer 5 — Backup & DR Health
- Backup job success  
- Backup repository capacity  
- Restore validation  
- Immutable copy verification  

---

## 4. Monitoring Tools

### 4.1 Windows Native Tools
- Event Viewer  
- Performance Monitor  
- AD DS Replication Status Tool  
- PKI Health Cmdlets  
- ADFS Admin Logs  
- Azure AD Connect Health  

### 4.2 Hypervisor Tools
- Hyper‑V Manager  
- ESXi Host Client  
- ESXi Logs  
- VM performance graphs  

### 4.3 Network Tools
- Cisco CLI  
- `show ip route`  
- `show vlan`  
- `show interface`  
- `show logging`  
- `show access-lists`  

### 4.4 Backup Tools
- Veeam Community Edition  
- Backup job logs  
- Restore test logs  

### 4.5 Optional Future Tools
- Grafana  
- Prometheus  
- Zabbix  
- Elastic Stack  

---

## 5. Identity Monitoring

### 5.1 AD DS
- Replication health  
- SYSVOL health  
- DNS health  
- Kerberos errors  
- LDAP errors  

### 5.2 Azure AD Connect
- Sync errors  
- Password hash sync  
- Federation metadata  

---

## 6. PKI Monitoring

### 6.1 Issuing CA
- CA database health  
- Certificate issuance failures  
- CRL publication  
- AIA publication  
- Key protection  

### 6.2 Root CA
- Offline storage integrity  
- CRL publication schedule  

---

## 7. Federation Monitoring

### 7.1 ADFS
- Token signing certificate expiration  
- Token decrypting certificate expiration  
- Authentication failures  
- Metadata publication  

### 7.2 WAP
- Proxy trust  
- SSL certificate expiration  
- Federation endpoint reachability  

---

## 8. Hypervisor Monitoring

### 8.1 Hyper‑V
- Host CPU/RAM  
- VM CPU/RAM  
- VHDX latency  
- VM network throughput  

### 8.2 ESXi
- Host CPU/RAM  
- VM CPU/RAM  
- VMDK latency  
- VM network throughput  

---

## 9. Network Monitoring

### 9.1 WS‑3850 (Core)
- Routing table  
- VLAN status  
- ACL enforcement  
- Interface errors  
- SVI health  

### 9.2 C3560CG (OOB)
- OOB reachability  
- PAW reachability  
- Management VLAN  

### 9.3 Cisco 891F (WAN)
- WAN link health  
- NAT table  
- Firewall rules  

---

## 10. Backup & DR Monitoring
- Backup job success  
- Backup repository capacity  
- Restore test success  
- Immutable copy verification  
- DR simulation results  

---

## 11. Alerting Strategy
- Daily identity health check  
- Daily PKI health check  
- Daily backup job check  
- Weekly restore test  
- Monthly DR simulation  
- Certificate expiration alerts  
- Federation trust alerts  

---

## 12. Deliverables
- Monitoring Architecture Document  
- Monitoring dashboards  
- Backup job monitoring  
- Identity health monitoring  
- PKI health monitoring  
- Federation monitoring  
- Hypervisor monitoring  
- Network monitoring  

---

## 13. Acceptance Criteria
- All monitoring layers defined  
- Identity monitoring operational  
- PKI monitoring operational  
- Federation monitoring operational  
- Hypervisor monitoring operational  
- Network monitoring operational  
- Backup monitoring operational  
- Documentation complete  
