# Segmentation Model

## Purpose
To define how the network is segmented logically and physically.

## Components
- VLAN segmentation
- VRF segmentation (if applicable)
- Zone-to-VLAN mapping
- ACL segmentation
- Routing segmentation
- Firewall segmentation (future)

## Rules
- Every VLAN MUST map to a zone.
- Routing MUST enforce segmentation boundaries.
- ACLs MUST enforce segmentation rules.
- Diagrams MUST exist in `/docs/diagrams/network/`.

## Enforcement
Referenced by:
- vlan-plan.md
- homelab-routing-plan.md
- port-level-acl-plan.md
