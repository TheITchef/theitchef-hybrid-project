# Risk Assessment
## Last Updated: 2026-07-05

---

## 1. Overview
This document identifies technical, operational, security, project‑management, and human risks present in the hybrid homelab environment.  
It provides a structured foundation for mitigation planning and safe execution of all architecture and deployment tasks.

---

## 2. Scope
This assessment covers risks across:
- Identity services (AD DS, DNS, DHCP, Azure AD Connect, ADFS)
- PKI (Root CA, Issuing CA, certificate lifecycle)
- Network infrastructure (Cisco WS‑3850, C3560CG, 891F)
- Compute infrastructure (Hyper‑V, ESXi)
- Management networks (OOB, PAW)
- Automation (PowerShell, Terraform)
- Documentation and Git workflow

---

## 3. Technical Risks
From your uploaded document:

> “Misconfigured VLANs, routing loops, PKI misconfiguration, AD replication issues, Hyper‑V / ESXi mismatch, Azure AD Connect failures, OOB exposure, Terraform state corruption.”  


Technical risks include:
- Incorrect VLAN tagging or segmentation
- Inter‑VLAN routing failures
- PKI trust chain or template misconfiguration
- AD replication latency or topology issues
- Hyper‑V vs ESXi networking inconsistencies
- Azure AD Connect sync failures
- OOB network exposure to production VLANs
- Terraform state corruption or drift

---

## 4. Operational Risks
From your uploaded document:

> “Configuration drift, lack of rollback points, overlapping tasks, device state uncertainty, hardware failure.”  


Operational risks include:
- Untracked configuration changes
- Missing VM snapshots or rollback points
- Multi‑tasking causing inconsistent states
- Unknown switch or hypervisor configuration
- Hardware instability or failure

---

## 5. Security Risks
- PKI private key exposure  
- AD attack surface expansion  
- ADFS/WAP exposure to internet  
- OOB network incorrectly routed  
- PAW contamination  
- Weak identity posture during early deployment  

---

## 6. Project Management Risks
- Scope creep  
- Loss of structure  
- Documentation gaps  
- Branch mismanagement  
- Inconsistent commit discipline  

---

## 7. Human Risks
- Fatigue  
- Rushing steps  
- Assuming device state  
- Overconfidence  
- Skipping documentation  

---

## 8. Mitigation Strategy
From your uploaded document:

> “Strict documentation discipline, overview → scope → outcome, document before configuring, VM snapshots, verify Cisco configs, protect PKI keys, clean PAW usage, never assume device state, Git feature‑branch workflow, maintain rollback points.”  


Mitigation includes:
- Documentation-first workflow  
- Verified device state before changes  
- VM snapshots before major tasks  
- Strict PKI key protection  
- Clean PAW usage  
- Git feature-branch workflow  
- Regular rollback points  
- Cisco config verification  

---

## 9. Acceptance Criteria
- Risk Assessment stored under `docs/governance/`
- All risk categories documented
- Mitigation strategies included
- References to Master Document and Current State Assessment
- Updated as new risks emerge

---

## 10. References
- [[Master Document]]  
- [[Current State Assessment]]  
- Hybrid-Homelab-Project-Document.txt  
