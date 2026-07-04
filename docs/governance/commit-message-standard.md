# Commit Message Standard

## Purpose
To ensure all commits are consistent, traceable, and aligned with the Task Lifecycle SOP and Branch Naming Standard.

## General Rules
- Commit messages MUST be clear, concise, and action‑verb aligned.
- Every commit MUST relate to the task associated with the branch.
- Commits MUST NOT contain unrelated changes.
- Commits MUST follow the formatting rules below.

---

## Commit Message Format

### Required Structure

Task: <Task Name>
Status: <In Progress | Completed>
Summary: <Short description of the change>
Code


### Examples

Task: Define Security Zones and Trust Boundaries
Status: In Progress
Summary: Added initial zone definitions and trust boundary matrix.
Code


Task: VLAN Plan
Status: Completed
Summary: Finalized VLAN assignments and updated addressing dependencies.
Code


---

## Additional Guidelines
- Use **present tense** (“Add”, “Update”, “Fix”).
- Keep the summary under **80 characters**.
- If multiple commits are needed, each commit must represent a **logical unit of work**.
- Avoid “misc changes”, “update stuff”, “fix things”.

---

## Mapping to Task Lifecycle
| Lifecycle Stage | Commit Behavior |
|-----------------|-----------------|
| WIP             | Frequent commits allowed |
| Review          | Only correction commits |
| Done            | No commits (branch merged) |

---

## Enforcement
- All commits in PRs will be checked against this standard.
- Non‑compliant commits must be squashed or rewritten before merge.