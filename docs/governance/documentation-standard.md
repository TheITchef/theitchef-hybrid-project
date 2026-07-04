# Documentation Standard

## Purpose
To ensure all Markdown documentation across the project is consistent, readable, and aligned with enterprise architecture practices.

## File Naming Rules
- Use **lowercase**.
- Use **hyphens** between words.
- Use **action‑verb** or **domain‑specific** naming.
- Avoid spaces, underscores, or camelCase.

Examples:

define-security-zones.md
network-topology.md
vm-placement-plan.md
Code


---

## Required Document Structure

Every document MUST contain the following sections:

### 1. Title
Clear, descriptive, action‑verb aligned.

### 2. Overview
Short explanation of the document’s purpose.

### 3. Scope
What the document covers and does not cover.

### 4. Dependencies
List any documents or configurations required.

### 5. Deliverables
What the document produces (plans, diagrams, configs).

### 6. Detailed Content
The main body of the document.

### 7. Acceptance Criteria
Clear conditions for completion.

### 8. References / Cross‑Links
Links to related documents.

---

## Formatting Rules
- Use `##` for main sections.
- Use `###` for subsections.
- Avoid deep nesting beyond `###`.
- Use bullet lists for clarity.
- Use tables for structured data.
- Use diagrams from `/docs/diagrams/` when applicable.

---

## Diagram Rules
- All diagrams MUST be stored under:

docs/diagrams/<domain>/
Code

- Diagrams MUST have a corresponding `.md` explanation file.
- Diagrams MUST be referenced in the main document.

---

## Cross‑Linking Rules
Use relative links:

[Looks like the result wasn't safe to show. Let's switch things up and try something else!]
Code


---

## Versioning Rules
- Major changes require a new commit with clear summary.
- Breaking changes require updating the governance index.

---

## Enforcement
- All new documents MUST follow this standard.
- Non‑compliant documents must be revised before merge.