# Kanban Workflow Structure  
Hybrid Homelab Project — Governance Document  
Version: 2026-07-02  
Author: Ioannis Mintzivyris

This document defines the authoritative Kanban workflow used for all project execution within the Hybrid Homelab.  
It enforces discipline, prevents multitasking, ensures documentation-first execution, and aligns with enterprise-grade governance principles.

---

## 1. Column Definitions

### 1.1 BACKLOG (Max 9)
The intake zone for all future work.  
Cards here are not ready for execution and may require clarification, scoping, or decomposition.

**Rules**
- Maximum 9 items.
- No execution from Backlog.
- Cards must be groomed before moving to Ready.

---

### 1.2 READY
Tasks that are fully understood, scoped, and prepared for prioritization.

**Rules**
- Cards must include: Overview, Scope, Expected Outcome.
- No execution from Ready.
- Cards move to Priority List only when actionable.

---

### 1.3 PRIORITY LIST (Max 3)
The short-term execution queue.  
Only the next 1–3 tasks intended for execution.

**Rules**
- Maximum 3 items.
- Cards here are candidates for Doing.
- No documentation or execution yet.

---

### 1.4 DOING (Max 2)
Active work in progress.  
This is where execution happens.

**Rules**
- Maximum 2 items.
- Documentation-first execution.
- Rollback points created when required.
- Git feature-branch workflow enforced.
- No multitasking beyond WIP limit.

---

### 1.5 REVIEW
Architectural validation stage.  
Cards must pass governance checks before entering Done.

**Purpose**
To ensure every completed task meets enterprise-grade standards.

**Rules**
- Cards must include Review Notes.
- Documentation must be complete.
- Git commits must be clean and pushed.
- Rollback points must be validated.
- Dependencies and risks must be documented.
- Only the architect role moves cards to Done.
- A global “REVIEW CHECKLIST” card must remain at the top of this column.

---

### 1.6 DONE
Completed work that meets all architectural, documentation, and governance requirements.

**Rules**
- Cards must pass Review stage.
- Documentation must be final.
- Git branch merged (if applicable).
- Rollback point confirmed.

---

## 2. Required Card Structure

Every card must contain the following sections:

### 2.1 Overview
What the task is and why it exists.

### 2.2 Scope
What is included and excluded.

### 2.3 Expected Outcome
Clear, measurable result.

### 2.4 Execution Notes
Steps taken, configurations verified, decisions made.

### 2.5 Documentation
Links or references to updated documentation.

### 2.6 Rollback Point
Snapshot/tag information if applicable.

### 2.7 Review Notes
Validation performed during Review stage.

---

## 3. Workflow Summary

Backlog → Ready → Priority → Doing → Review → Done
Code


This workflow ensures:

- Predictable flow  
- Documentation-first discipline  
- Architectural governance  
- Clean Git workflow  
- Safe rollback strategy  
- Enterprise-grade execution  

---

## 4. Governance Notes

- The Kanban board itself lives in the Obsidian vault.  
- This document lives in the Git repository as the authoritative workflow definition.  
- All changes to this workflow must be documented through an ADR (Architecture Decision Record).