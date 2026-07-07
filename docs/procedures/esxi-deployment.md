# ESXi Deployment Procedure
Version: 2026‑07‑07  
Author: Ioannis Mintzivyris  
Location: Stora Wäsby, Stockholm County, Sweden

---

## 1. Purpose
This procedure defines the full lifecycle steps required to deploy an ESXi hypervisor host in the homelab environment, aligned with the Compute Architecture, Network Topology, VLAN & Trunking Strategy, VM Placement Plan, PKI Architecture, and Security Architecture Standard.

---

## 2. Scope
This procedure applies to:
- ESXi01 (Dell PowerEdge R620)
- ESXi02 (Dell PowerEdge R620)
- Any future ESXi hosts added to the homelab

---

## 3. Prerequisites
- AD DS deployment completed  
- Homelab Architecture Overview defined  
- VLAN Plan defined  
- Trunking Strategy defined  
- VM Placement Plan defined  
- PKI Root CA available  
- PAW reachability validated  
- OOB management validated  
- Switch port trunking configured according to design  

---

## 4. Hardware Requirements
- Dell PowerEdge R620  
- RAID1 boot volume  
- RAID10 or RAID5 datastore volume  
- Dual 1GbE or 10GbE NICs  
- iDRAC Enterprise license  
- BIOS configured for virtualization (VT‑x, VT‑d enabled)

---

## 5. Network Requirements
- Management VLAN  
- vMotion VLAN  
- Storage VLAN (optional)  
- VM VLANs according to VM Placement Plan  
- Trunking configured on upstream switch ports  
- NTP reachable from management network  

---

## 6. Security Requirements
- Root password meets Homelab Security Standard  
- SSH disabled unless required  
- Lockdown Mode optional  
- PKI root CA installed  
- NTP configured to internal or trusted source  

---

# 7. ESXi Deployment Procedure (Step‑by‑Step)

## Step 1 — Prepare Host Hardware
1. Boot into iDRAC.  
2. Verify CPU virtualization extensions enabled.  
3. Configure RAID:
   - RAID1 for ESXi boot  
   - RAID10 or RAID5 for datastore  
4. Update BIOS and firmware to latest stable versions.  
5. Set boot mode to UEFI.

---

## Step 2 — Install ESXi
1. Mount ESXi ISO via iDRAC Virtual Media.  
2. Boot from Virtual CD/DVD.  
3. Select target RAID1 boot volume.  
4. Set root password according to Security Standard.  
5. Complete installation and reboot.  
6. Remove Virtual Media to avoid boot loops.

---

## Step 3 — Initial Host Configuration
1. Press **F2** → Configure Management Network.  
2. Assign static IP from Management VLAN.  
3. Configure:
   - Subnet mask  
   - Default gateway  
   - DNS servers  
4. Set hostname:  
   - `esxi01.lab.theitchef.com`  
   - `esxi02.lab.theitchef.com`  
5. Enable NTP and set server to internal or trusted source.  
6. Test network connectivity.

---

## Step 4 — Configure vSwitches and VMkernel Interfaces
### vSwitch0 (Management)
- vmnic0  
- VLAN ID: Management VLAN  
- VMkernel: `Management`  
- Services: Management, vSphere API

### vSwitch1 (vMotion)
- vmnic1  
- VLAN ID: vMotion VLAN  
- VMkernel: `vMotion`  
- Services: vMotion

### vSwitch2 (VM Networks)
- vmnic2, vmnic3 (if available)  
- VLANs according to VM Placement Plan  
- Port groups created per VM VLAN

---

## Step 5 — Configure Storage (Optional)
If using NFS or iSCSI:
1. Create VMkernel interface on Storage VLAN.  
2. Add NFS or iSCSI target.  
3. Validate datastore visibility.

---

## Step 6 — Apply Security Hardening
1. Disable SSH unless required.  
2. Disable ESXi Shell unless required.  
3. Configure Lockdown Mode (optional).  
4. Install PKI root CA certificate.  
5. Validate certificate chain.

---

## Step 7 — Validate Networking
1. Ping gateway from Management VMkernel.  
2. Ping vMotion VMkernel between hosts.  
3. Validate VLAN tagging using:

esxcli network nic list
esxcli network vswitch standard list
Code

4. Validate VM placement VLAN reachability.

---

## Step 8 — Add Host to vCenter (If applicable)
1. Log into vCenter.  
2. Add ESXi host using FQDN.  
3. Validate:
- Datastores  
- VMkernel interfaces  
- vSwitches  
- Host health  

---

## Step 9 — Documentation Update
1. Update:
- VM Placement Plan  
- VLAN & Trunking Plan  
- Switch Port Mapping  
- Compute Architecture  
2. Commit changes to repo following:
- Branch Naming Standard  
- Commit Message Standard  

---

## 8. Post‑Deployment Validation
- Host reachable from PAW  
- Host reachable from management VLAN  
- vSwitches configured correctly  
- VMkernel interfaces reachable  
- VLAN tagging validated  
- Datastores visible  
- VM placement validated  
- Host added to vCenter (if applicable)  
- Documentation updated  

---

## 9. References
- Compute Architecture  
- Network Topology  
- VLAN Plan  
- Trunking Strategy  
- VM Placement Plan  
- PKI Architecture  
- Security Architecture Standard  
