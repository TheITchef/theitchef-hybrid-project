# Logical Network Diagram
Version: 2026‑07‑07

## 1. Purpose
Provide a high‑level logical network diagram describing VLANs, routing, firewall boundaries, and core infrastructure relationships.  
This diagram is the authoritative reference for network architecture.

---

## 2. Diagram Overview (Textual Representation)

+----------------------+
|      Internet        |
+----------+-----------+
|
|
+----------v-----------+
|      Firewall        |
|  Inside: 10.10.50.253|
|  DMZ:    10.10.80.254|
+----------+-----------+
|
|
+----------------v----------------+
|         Core Switch             |
|        Cisco 3850 L3            |
+----------------+----------------+
|
-----------------------------------------------------------------
|              |              |              |                  |
|              |              |              |                  |
+----v----+    +----v----+    +----v----+    +----v----+      +-----v-----+
| VLAN10  |    | VLAN20  |    | VLAN30  |    | VLAN40  |      | VLAN50    |
| MGMT    |    | VMOTION |    | STORAGE |    | SRV-VM  |      | INFRA-VM  |
+---------+    +---------+    +---------+    +---------+      +-----------+

+---------+    +---------+    +---------+    +---------+      +-----------+
| VLAN60  |    | VLAN70  |    | VLAN80  |    | VLAN90  |      | VLAN100   |
| PAW     |    | USER    |    | DMZ     |    | MONITOR |      | BACKUP    |
+---------+    +---------+    +---------+    +---------+      +-----------+
Code


---

## 3. Key Components

### **Firewall**
- Enforces DMZ ↔ Internal boundaries  
- Default route for core switch  
- Performs NAT for outbound traffic  

### **Core Switch (Cisco 3850)**
- L3 routing  
- SVI gateways  
- ACL enforcement  
- Trunk uplinks to ESXi  

### **ESXi Hosts**
- Connected via dual trunk uplinks  
- Carry VLANs 10,20,30,40,50  

### **Infrastructure VMs**
- AD DS, PKI, ADFS, WAP  
- Located in VLAN50  

### **Server VMs**
- Located in VLAN40  

### **PAWs**
- Located in VLAN60  

### **User Endpoints**
- Located in VLAN70  

### **DMZ Servers**
- Located in VLAN80  

### **Monitoring & Backup**
- VLAN90 and VLAN100 respectively  

---

## 4. Notes
- Diagram aligns with VLAN, addressing, routing, ACL, zones, and port mapping documents.  
- This is the authoritative logical view of the homelab network.  