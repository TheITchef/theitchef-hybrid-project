# Monitoring Architecture
Version: 2026‑07‑07

## 1. Purpose
Define the monitoring architecture for the homelab, including components, data flows, trust boundaries, and integration with all network zones.

---

## 2. Monitoring Zone (VLAN 90)
- Subnet: 10.10.90.0/24  
- Gateway: 10.10.90.1  
- Trust Level: Medium‑High  
- Read‑only access to all zones (enforced by ACLs)

---

## 3. Monitoring Components

### **MON01 (Primary Monitoring Server)**
- IP: 10.10.90.11  
- Role: Metrics, logs, alerts  
- Services:
  - Prometheus  
  - Grafana  
  - Loki / syslog ingestion  
  - Telegraf agents  
  - SNMP polling  

### **Backup Monitoring Node**
- IP: 10.10.90.12  
- Role: Secondary collector, dashboard replication

---

## 4. Data Collection Methods

### **1. SNMP Polling**
Used for:
- Switches  
- Router  
- Firewall  
- ESXi hosts  

SNMP community: `readonly-monitoring`

### **2. Syslog**
Sent from:
- Switches → 10.10.90.11  
- Firewall → 10.10.90.11  
- Router → 10.10.90.11  

### **3. Agent-Based Metrics**
- Telegraf installed on:
  - DC01  
  - DC02  
  - PKI01  
  - ADFS01  
  - WAP01  
  - Server VMs  

### **4. ESXi Integration**
- vCenter API polling  
- ESXi host metrics via CIM  

---

## 5. Monitoring Data Flows (Logical)

+------------------+        Syslog/SNMP/API        +----------------------+
| Switches/Router  | ----------------------------> | MON01 (10.10.90.11)  |
+------------------+                                +----------------------+

+------------------+        Telegraf Agents        +----------------------+
| Infra VMs        | ----------------------------> | MON01                |
+------------------+                                +----------------------+

+------------------+        vCenter API            +----------------------+
| ESXi Hosts       | ----------------------------> | MON01                |
+------------------+                                +----------------------+
Code


---

## 6. Trust Boundaries

### **Monitoring → All Zones**
- Allowed: Read‑only  
- Denied: Write, management, configuration  
- Enforced via ACLs:
  - `permit ip 10.10.90.0/24 any` (read-only flows)
  - No reverse flows initiated from monitored zones

### **DMZ → Monitoring**
- Allowed: Syslog only  
- Denied: SNMP, API, metrics  

---

## 7. Alerting Pipeline

### **Alert Sources**
- Prometheus alert rules  
- Syslog severity filters  
- Firewall event triggers  

### **Alert Destinations**
- Email → admin@lab.theitchef.com  
- Slack webhook (optional)  
- Dashboard alerts in Grafana  

---

## 8. Notes
- Monitoring zone is read‑only by design.  
- All monitoring flows align with ACL Plan and Security Zones.  
- MON01 is the authoritative collector for all telemetry.  