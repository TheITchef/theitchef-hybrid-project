# Monitoring Implementation Plan
Version: 2026‑07‑07  
Author: Ioannis Mintzivyris

## 1. Purpose
Define the implementation plan for deploying, integrating, and operationalizing the monitoring stack described in `monitoring-architecture.md`.  
This plan covers rollout sequencing, configuration tasks, validation, and operational readiness.

---

## 2. Scope
This implementation plan applies to:

- MON01 (Primary Monitoring Server)
- MON02 (Secondary Monitoring Server)
- WS‑3850 Core Switch
- Cisco 891F Router
- Firewall (Inside + DMZ)
- ESXi01 Hypervisor
- Infrastructure VMs (DC01, DC02, PKI01, ADFS01, WAP01)
- Server VMs
- PAWs
- DMZ servers

---

## 3. Implementation Phases

### **Phase 1 — Infrastructure Preparation**
- Ensure VLAN90 (Monitoring) is reachable from all zones  
- Validate SVI: `10.10.90.1`  
- Validate DNS entries:
  - `mon01.lab.theitchef.com`
  - `mon02.lab.theitchef.com`
- Validate firewall rules:
  - Allow syslog → MON01
  - Allow SNMP → MON01
  - Allow HTTPS → Grafana

### **Phase 2 — MON01 Deployment**
1. Install Ubuntu Server LTS  
2. Configure hostname:

hostnamectl set-hostname mon01.lab.theitchef.com
Code

3. Configure static IP:

10.10.90.11/24
GW: 10.10.90.1
DNS: 10.10.50.11
Code

4. Install monitoring stack:
- Prometheus  
- Grafana  
- Loki  
- Telegraf (for local metrics)  
5. Enable and start services

### **Phase 3 — MON02 Deployment (Optional Redundancy)**
- Deploy identical OS + stack  
- Configure IP: `10.10.90.12`  
- Configure replication (Loki, dashboards)

### **Phase 4 — Network Device Integration**
#### Switches (WS‑3850)
- Configure syslog:

logging host 10.10.90.11
Code

- Configure SNMP:

snmp-server community readonly-monitoring RO
snmp-server host 10.10.90.11 version 2c readonly-monitoring
Code


#### Router (Cisco 891F)
- Configure syslog:

logging 10.10.90.11
Code

- Configure SNMP:

snmp-server community readonly-monitoring RO
Code


#### Firewall
- Configure syslog → MON01  
- Allow SNMP only from MON01  
- Deny SNMP from all other zones

### **Phase 5 — ESXi + vCenter Integration**
- Enable SNMP on ESXi:

esxcli system snmp set --communities readonly-monitoring
esxcli system snmp set --enable true
Code

- Deploy Prometheus vSphere exporter  
- Validate metrics ingestion

### **Phase 6 — VM Agent Deployment**
Install Telegraf on:

- DC01  
- DC02  
- PKI01  
- ADFS01  
- WAP01  
- Server VMs  

Configure Prometheus output:

[[outputs.prometheus_client]]
listen = ":9273"
Code


### **Phase 7 — DMZ Integration**
- Allow syslog only  
- Deny SNMP  
- Deny API polling  
- Validate DMZ → MON01 syslog flow

### **Phase 8 — Dashboard & Alerting Setup**
- Import baseline dashboards:
  - ESXi host metrics  
  - VM metrics  
  - Network device metrics  
  - Syslog viewer  
- Configure alerting:
  - Email → admin@lab.theitchef.com  
  - Optional Slack webhook  
- Validate alert triggers

---

## 4. Validation Checklist

### **Network Reachability**
- MON01 reachable from all VLANs  
- SNMP reachable only from MON01  
- Syslog flows validated  

### **Metrics Collection**
- Prometheus targets show “UP”  
- Telegraf endpoints reachable  
- vSphere exporter reachable  

### **Logs**
- Loki receiving syslog  
- Grafana logs dashboard populated  

### **Alerts**
- Test alert → email  
- Test alert → Slack (optional)  

---

## 5. Operational Handover
- Document dashboard locations  
- Document alerting rules  
- Document SNMP communities  
- Document syslog sources  
- Add monitoring to daily operational checklist  

---

## 6. Notes
- MON01 is authoritative collector  
- MON02 optional for redundancy  
- Monitoring zone is read‑only by design  
- All flows must align with ACL Plan and Security Zones  

