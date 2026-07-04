# Branch Naming Standard

## Purpose
To ensure consistent, predictable, and traceable branch names across the entire homelab project.  
This standard aligns with the Task Lifecycle SOP and the Kanban workflow.

## General Rules
- All branch names use **lowercase**.
- Words are separated using **hyphens**.
- Branch names must be **action‑verb aligned**.
- Branch names must map directly to a **single task**.
- Branch names must never contain spaces.
- Branch names must be short, descriptive, and unambiguous.

---

## Branch Categories

### 1. Feature Branches
Used for new tasks, design work, documentation creation, or new functionality.

Format:

feature/<action-verb-task-name>
Code


Examples:

feature/define-security-zones-and-trust-boundaries
feature/create-vlan-plan
feature/update-routing-design
feature/document-esxi-networking
Code


---

### 2. Fix Branches
Used for corrections, bug fixes, or adjustments to existing content.

Format:

fix/<issue-or-correction>
Code


Examples:

fix/correct-vlan-id
fix/update-port-mapping-errors
fix/typo-in-pki-architecture
Code


---

### 3. Docs Branches
Used for documentation-only changes that are not part of a feature task.

Format:

docs/<documentation-topic>
Code


Examples:

docs/update-governance-index
docs/add-security-architecture
docs/revise-network-topology
Code


---

### 4. Refactor Branches
Used for restructuring code, reorganizing folders, or improving existing content without changing functionality.

Format:

refactor/<component-or-area>
Code


Examples:

refactor/powershell-modules
refactor/terraform-environments
refactor/network-docs-structure
Code


---

### 5. Hotfix Branches
Used for urgent corrections that must be applied immediately.

Format:

hotfix/<critical-issue>
Code


Examples:

hotfix/broken-routing-diagram
hotfix/missing-pki-config
Code


---

## Mapping to Kanban Workflow

| Kanban Stage | Branch Action |
|--------------|---------------|
| Ready → Priority | No branch yet |
| Priority → WIP | Create feature/… branch |
| WIP → Review | Work stays in branch |
| Review → Done | Merge branch → delete branch |

---

## Branch Lifecycle Rules
- One task = one branch  
- Branch must be deleted after merge  
- Branch must never contain unrelated changes  
- Branch must follow the Task Lifecycle SOP  
- Branch must be created **only** when the task enters WIP

---

## Storage Location in Repo

This standard must be stored in:

docs/governance/branch-naming-standard.md
Code


This location is consistent with:
- `task-lifecycle.md`
- `kanban-workflow-structure.md`
- `project-charter.md`
- `scope-and-requirements.md`

It becomes part of your **governance framework**.
