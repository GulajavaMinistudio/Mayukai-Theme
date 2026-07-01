---
name: bug-remediation-architect
description: "Workflow for analyzing bug reports, tracing root causes, and generating structured bug-fix implementation plans with rollback strategies."
license: MIT
---
<!-- markdownlint-disable -->
# Bug Remediation Architect Skill

## Overview
This skill outlines the diagnostic workflow to investigate reported bugs, identify root causes, and generate formal, executable implementation plans to fix them safely. It prioritizes Test-Driven Bug Fixing and rollback planning. This skill accompanies the `@BugRemediationArchitect` agent.

## When to Use
- When investigating a reported bug or issue in the codebase.
- When generating a structured bug-fix plan in the `/plan/` directory.

---

## Phase 1: Bug Investigation & Root Cause Analysis Workflow

1. **Information Gathering & Simulation:** Read and understand the symptoms. Reproduce the bug if possible, or simulate the scenario by tracing the code logic using search and read tools.
2. **Root Cause Identification:** Pinpoint the exact file, function, and logic error causing the issue.
3. **Determine Minimal Fix:** Formulate a solution that fixes the root cause with the least amount of code changes. Consider edge cases and potential regressions.
4. **Present Findings:** Output your diagnosis in the chat using the following structured format (in Bahasa Indonesia):
   - **Laporan Masalah (Issue Summary):** A brief restatement of the bug.
   - **Akar Masalah (Root Cause):** Detailed technical explanation of *why* the bug occurs. Mention specific files and lines of code.
   - **Strategi Perbaikan (Remediation Strategy):** How you plan to fix it minimally.
5. **Discuss Strategy:** Ensure the user agrees with your diagnosis and proposed fix before moving to Phase 2.

---

## Phase 2: Fix Plan Generation Workflow

1. Ask the user (in Bahasa Indonesia): *"Saya telah menemukan akar masalahnya. Apakah Anda ingin saya membuat dokumen Implementation Plan resmi untuk memperbaiki bug ini?"*
2. **Filename:** Use the naming convention `bug-fix-YYYYMMDD-[short-description].md` (e.g., `bug-fix-20260603-auth-crash.md`) and save it in the `/plan/` directory.
3. **Template:** The file MUST strictly adhere to the template below, enforcing step-by-step execution, testing, rollback strategies, and mandatory approval checkpoints.

---

## Mandatory Bug Fix Plan Template

```md
---
goal: [Concise Title Describing the Bug Fix]
version: [Optional: e.g., 1.0, Date]
date_created: [YYYY-MM-DD]
last_updated: [Optional: YYYY-MM-DD]
owner: [Optional: Team/Individual responsible for this spec]
status: "Planned"
tags: ["bug-fix", "remediation", "patch"]
---

# Introduction

![Status: <status>](https://img.shields.io/badge/status-<status>-<status_color>)

[A short concise introduction to the bug being addressed, its impact, and the root cause that was identified during analysis.]

## 1. Requirements & Constraints (Fix Constraints)

[Explicitly list the constraints for this bug fix, ensuring no regressions are introduced.]

- **REQ-001**: The fix must resolve [Specific Issue].
- **CON-001**: The fix must not alter the existing public API response structure.
- **CON-002**: Backward compatibility must be maintained.

## 2. Implementation Steps

> **⚠️ EXECUTION DIRECTIVE FOR AI AGENTS:** 
> You MUST execute this plan phase by phase. You MUST run the specific testing/verification task at the end of each phase. After a phase is tested, you **MUST STOP AND WAIT** for the user's explicit approval before proceeding to the next phase.

### Implementation Phase 1: Test Writing (Test-Driven Bug Fixing)
- GOAL-001: Write a failing test that reproduces the exact bug described.

| Task     | Description                                                             | Completed | Date |
| -------- | ----------------------------------------------------------------------- | --------- | ---- |
| TASK-001 | Write unit/integration test to reproduce the bug                        |           |      |
| TASK-00X | **VERIFY**: Run the test. It MUST FAIL.                                 |           |      |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed to Phase 2 |           |      |

### Implementation Phase 2: Minimal Root Cause Remediation
- GOAL-002: Implement the core logic fix in the production code without over-engineering.

| Task     | Description                                                  | Completed | Date |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| TASK-002 | Apply the minimal fix to [Specific File/Function]            |           |      |
| TASK-003 | Clean up any adjacent code affected by the fix               |           |      |
| TASK-00X | **VERIFY**: Run the test from Phase 1. It MUST PASS.         |           |      |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed |           |      |

## 3. Rollback Strategy

[Describe the exact steps to revert this fix if it causes unexpected issues in production or breaks related systems.]

- **RBCK-001**: Step 1 to revert changes.
- **RBCK-002**: Step 2 to restore previous state.

## 4. Dependencies

[List any dependencies that need to be updated as part of this fix.]

- **DEP-001**: Dependency 1

## 5. Files Affected

[List all files that will be modified to fix this bug.]

- **FILE-001**: Description of file 1

## 6. Testing Strategy & Edge Cases

[Describe how this bug will be prevented from recurring in the future and note any specific edge cases considered during the fix.]

- **TEST-001**: Description of test strategy

## 7. Risks & Assumptions

[List any risks related to this fix, such as potential side effects on other modules.]

- **RISK-001**: Risk 1
```
