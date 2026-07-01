---
name: expert-code-reviewer
description: "Language-agnostic workflow for code reviews and security audits against Clean Code/SOLID principles, generating formal refactoring plans."
license: MIT
---
<!-- markdownlint-disable -->
# Expert Code Reviewer Skill

## Overview
This skill provides the structured workflow for analyzing codebase implementations, identifying architectural flaws, detecting security vulnerabilities, and generating formal, executable implementation plans for refactoring and remediation. This skill accompanies the `@ExpertCodeReviewer` agent.

## When to Use
- When the coding phase is complete and needs a comprehensive audit.
- When security vulnerabilities or code smells are suspected.
- When you need to create a structured refactoring plan in the `/plan/` directory.

---

## Phase 1: Code & Security Review Workflow

1. **Evaluate Against Clean Code & SOLID:** Check for meaningful naming, function size, proper abstractions, error handling, and adherence to SOLID principles.
2. **Security Scan:** Look for injection risks, insecure data handling, hardcoded secrets, and improper authorization (OWASP Top 10).
3. **Present Findings:** Output your review in the chat using the following structured format (in Bahasa Indonesia):
   - **Summary (Ringkasan):** Brief overview of the code's quality.
   - **Detailed Findings (Temuan Detail):** For each issue:
     - **Issue (Isu):** Description.
     - **Category (Kategori):** Clean Code / SOLID / Security / Other.
     - **Severity (Tingkat Keparahan):** Low (Rendah) / Medium (Sedang) / High (Tinggi).
     - **Location (Lokasi):** Line numbers or function names.
     - **Recommendation (Rekomendasi):** Concrete approach to fix it.
4. **Discuss Strategy:** Discuss the refactoring strategy with the user and ensure they agree before moving to Phase 2.

---

## Phase 2: Implementation Plan Generation Workflow

1. Ask the user (in Bahasa Indonesia): *"Saya telah menyelesaikan review. Apakah Anda ingin saya membuat dokumen Implementation Plan resmi untuk perbaikan dan refactoring ini?"*
2. **Filename:** Use the naming convention `refactor-[component]-[version].md` and save it in the `/plan/` directory.
3. **Template:** The file MUST strictly adhere to the template below, enforcing step-by-step execution and mandatory approval checkpoints.

---

## Mandatory Refactoring Plan Template

```md
---
goal: [Concise Title Describing the Refactoring & Security Plan's Goal]
version: [Optional: e.g., 1.0, Date]
date_created: [YYYY-MM-DD]
last_updated: [Optional: YYYY-MM-DD]
owner: [Optional: Team/Individual responsible for this spec]
status: "Planned"
tags: ["refactor", "clean-code", "architecture", "security"]
---

# Introduction

![Status: <status>](https://img.shields.io/badge/status-<status>-<status_color>)

[A short concise introduction to the refactoring plan, the technical debt being addressed, the architectural goal, and any security vulnerabilities being remediated.]

## 1. Requirements & Constraints (Architecture & Security Focus)

[Explicitly list the architectural and security principles guiding this refactoring.]

- **REQ-001**: Requirement 1
- **PRN-001**: Architectural Principle (e.g., Ensure Single Responsibility Principle)
- **SEC-001**: Security Requirement (e.g., Prevent SQL Injection via parameterized queries)
- **CON-001**: Constraint 1

## 2. Implementation Steps

> **⚠️ EXECUTION DIRECTIVE FOR AI AGENTS:** 
> You MUST execute this plan phase by phase. You MUST run the specific testing/verification task at the end of each phase. After a phase is tested, you **MUST STOP AND WAIT** for the user's explicit approval before proceeding to the next phase.

### Implementation Phase 1: Security Remediation & Decoupling
- GOAL-001: [Describe the goal of this phase]

| Task     | Description                                                             | Completed | Date |
| -------- | ----------------------------------------------------------------------- | --------- | ---- |
| TASK-001 | Description of task 1 (include exact file paths)                        |           |      |
| TASK-00X | **VERIFY**: [Specific testing/verification step for this phase]         |           |      |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed to Phase 2 |           |      |

### Implementation Phase 2: Core Architectural Refactoring
- GOAL-002: [Describe the goal of this phase]

| Task     | Description                                                     | Completed | Date |
| -------- | --------------------------------------------------------------- | --------- | ---- |
| TASK-003 | Description of task 3                                           |           |      |
| TASK-00X | **VERIFY**: [Specific testing/verification step for this phase] |           |      |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed    |           |      |

## 3. Alternatives

[A bullet point list of any alternative architectural/security approaches considered.]
- **ALT-001**: Alternative approach 1

## 4. Dependencies

[List any new dependencies introduced or removed, including security libraries or sanitization packages.]
- **DEP-001**: Dependency 1

## 5. Files Affected

[List all files that will be modified, deleted, or created.]
- **FILE-001**: Description of file 1

## 6. Testing

[List the tests that need to be updated or implemented to verify behavior and ensure security vulnerabilities are patched. Phase-specific tests are in the Implementation Steps.]
- **TEST-001**: Description of test 1

## 7. Risks & Assumptions

[List any risks related to the refactoring or potential edge cases in the security patch.]
- **RISK-001**: Risk 1
```
