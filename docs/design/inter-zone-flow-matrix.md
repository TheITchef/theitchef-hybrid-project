# Inter‑Zone Flow Matrix

## Purpose
To define all permitted flows between zones and enforce least privilege.

## Matrix Fields
- Source Zone
- Destination Zone
- Protocol
- Port
- Purpose
- ACL Action (Allow/Deny)
- Notes

## Rules
- No flow is allowed unless explicitly documented.
- ACLs MUST be generated from this matrix.
- Changes MUST trigger ACL updates.

## Enforcement
Referenced by:
- ACL tables
- segmentation-model.md
- network-topology.md
