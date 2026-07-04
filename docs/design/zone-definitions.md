# Zone Definitions

## Purpose
To define all logical and physical security zones in the hybrid homelab.

## Required Fields per Zone
- Zone Name
- Purpose
- Allowed Services
- Allowed Inbound Flows
- Allowed Outbound Flows
- Trust Level
- ACL Requirements

## Zones to Define
- Core Infrastructure Zone
- Identity Zone (AD/PKI)
- Management Zone
- Compute Zone (Hyper‑V / ESXi)
- DMZ / Edge Zone
- User Zone
- Storage Zone
- External Services Zone

## Enforcement
Zone definitions MUST be referenced by:
- trust-boundaries.md
- inter-zone-flow-matrix.md
- segmentation-model.md
- ACL tables
