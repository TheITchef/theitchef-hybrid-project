## Define Trunking Strategy — Kanban Card Body

### 📘 Purpose
Design the complete 802.1Q trunking model for the hybrid homelab environment.  
This task defines how VLANs are transported between switches, hypervisors, routers, PAWs, and OOB systems.  
It is a **design‑only** activity performed before any switch configuration or OS deployment.

### 🎯 Objectives
- Establish all trunk ports and their roles.
- Define allowed VLAN lists per trunk.
- Set native VLAN strategy (where applicable).
- Document ESXi01 tagging model.
- Clarify Router Inside trunking on Cisco 891F LAN FE ports.
- Enforce PAW and OOB isolation.
- Ensure alignment with physical cabling constraints.
- Produce a final trunking strategy document stored in the repo.

### 🧩 Scope
This task covers all links that may carry multiple VLANs:
- WS‑3850 ↔ WS‑3560CG inter‑switch uplink
- ESXi01 uplinks (R620‑01 only)
- Router Inside trunk (Cisco 891F LAN FE ports)
- PAW access port strategy
- OOB access ports
- Access ports for DC01, MS01, R620‑02 (unassigned hardware)

### 🔧 Key Design Decisions

#### 1. Inter‑Switch Trunk (3850 ↔ 3560CG)
- Mode: Trunk  
- Native VLAN: None  
- Allowed VLANs: 10, 20, 30, 40, 90, 99  
- Purpose: Core ↔ Access VLAN transport

#### 2. ESXi01 Uplinks (R620‑01)
- Mode: Trunk  
- Native VLAN: None  
- Allowed VLANs: 20, 30, 40  
- Tagging Model: All ESXi traffic tagged  
- Note: R620‑02 is unassigned hardware → no trunking

#### 3. Router Inside (Cisco 891F)
- Correct trunk port: LAN FE0/x (physically GE, logically FE)  
- Mode: Trunk  
- Native VLAN: None  
- Tagged VLANs: 90 (Router Inside)  
- WAN port GE0/8: Routed only → no trunking

#### 4. PAW
- Mode: Access  
- VLAN: 99  
- No tagging

#### 5. OOB / iDRAC / iLO
- Mode: Access  
- VLAN: 100  
- Strict isolation  
- No trunking

#### 6. Other Servers
- DC01 → Access VLAN 10  
- MS01 → Access VLAN TBD  
- R620‑02 → Access VLAN TBD (no OS, no role)

### 🏷 Native VLAN Strategy
| Link | Native VLAN | Reason |
|------|-------------|--------|
| 3850 ↔ 3560CG | None | Prevent untagged traffic |
| ESXi01 uplinks | None | ESXi uses full tagging |
| Router Inside | None | VLAN 90 tagged |
| OOB | 100 | Isolated management |

### 📄 Expected Output
A finalized trunking strategy document stored at:

`C:\Homelab\theitchef-hybrid-project\docs\design\define-trunking-strategy.md`

This document becomes the authoritative reference for:
- Port Mapping  
- Switch configuration  
- ESXi networking  
- Router Inside integration  
- Future SOPs  

### ✔ Completion Criteria
- All trunk ports defined  
- Allowed VLAN lists finalized  
- Native VLAN strategy documented  
- ESXi01 tagging model defined  
- Router Inside trunking clarified  
- PAW and OOB isolation enforced  
- Document saved in repo  
- Card ready to move from **WIP → Done**


