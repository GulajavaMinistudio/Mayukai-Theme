---
name: planner-architect
description: "Generates formal, structured, and executable implementation plan documents based on specifications."
license: MIT
---
<!-- markdownlint-disable -->
# Planner Architect Skill

## Overview
This skill outlines the workflow to transform technical specifications and requirements into formal, structured, and executable implementation plans. It ensures plans are machine-readable and highly deterministic. This skill accompanies the `@PlannerArchitect` agent.

## When to Use
- When the Technical Specification phase is complete and you need to break down the work into actionable tasks.
- When you need to create a step-by-step roadmap before actual coding (`@GodModeDev`) begins.
- When generating files in the `/plan/` directory.

---

## Phase 1: Strategic Discussion & Analysis Workflow

1.  **Start with Understanding:**
    - **Check for Specs:** Look for a formal technical specification document (e.g., in `/spec/`). If it exists, you **MUST read and deeply analyze it** to align with its data contracts and constraints.
    - Clarify goals and identify affected components.
2.  **Analyze Before Planning:**
    - Review existing codebase patterns and test coverage.
3.  **Develop Strategy Collaboratively:**
    - Break down complex requirements into manageable components.
    - Propose a clear approach, discussing edge cases and mitigations.

---

## Phase 2: Implementation Plan Generation Workflow

1.  Offer the user: "I have gathered all the necessary information. Would you like me to generate the formal Implementation Plan file?"
2.  If agreed, create the new file using the strictly defined file naming convention (`[purpose]-[component]-[version].md`) and save it in the `/plan/` directory.
3.  Purpose prefixes: `upgrade|refactor|feature|data|infrastructure|process|architecture|design`.
4.  **Content:** The file's content **MUST** adhere to the Mandatory Implementation Plan Template below.

---

## AI-Optimized Implementation Standards

- **Phase Architecture (Strict Enforcement):** Each phase MUST conclude with a testing task and a **mandatory checkpoint (APPROVAL)** requiring explicit user approval before proceeding.
- Use explicit, unambiguous, and machine-parseable language (tables, lists).
- Include specific file paths, function names, and line numbers.

---

## Mandatory Implementation Plan Template

```md
---
goal: [Concise Title Describing the Package Implementation Plan's Goal]
version: [Optional: e.g., 1.0, Date]
date_created: [YYYY-MM-DD]
last_updated: [Optional: YYYY-MM-DD]
owner: [Optional: Team/Individual responsible for this spec]
status: 'Completed'|'In progress'|'Planned'|'Deprecated'|'On Hold'
tags: [Optional: List of relevant tags or categories, e.g., `feature`, `upgrade`, `chore`, `architecture`, `migration`, `bug` etc]
---

# Introduction

![Status: <status>](https://img.shields.io/badge/status-<status>-<status_color>)

[A short concise introduction to the plan and the goal it is intended to achieve.]

## 1. Requirements & Constraints

[Explicitly list all requirements & constraints that affect the plan. Use bullet points or tables.]
- **REQ-001**: Requirement 1
- **SEC-001**: Security Requirement 1
- **CON-001**: Constraint 1

## 2. Implementation Steps

> **⚠️ EXECUTION DIRECTIVE FOR AI AGENTS:** 
> You MUST execute this plan phase by phase. You MUST run the specific testing/verification task at the end of each phase. After a phase is tested, you **MUST STOP AND WAIT** for the user's explicit approval before proceeding to the next phase.

### Implementation Phase 1
- GOAL-001: [Describe the goal of this phase]

| Task     | Description                                                             | Completed | Date       |
| -------- | ----------------------------------------------------------------------- | --------- | ---------- |
| TASK-001 | Description of task 1                                                   |           |            |
| TASK-00X | **VERIFY**: [Specific testing/verification step for this phase]         |           |            |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed to Phase 2 |           |            |

### Implementation Phase 2
- GOAL-002: [Describe the goal of this phase]

| Task     | Description                                                     | Completed | Date |
| -------- | --------------------------------------------------------------- | --------- | ---- |
| TASK-002 | Description of task 2                                           |           |      |
| TASK-00X | **VERIFY**: [Specific testing/verification step for this phase] |           |      |
| TASK-00Y | **APPROVAL**: Wait for explicit user confirmation to proceed    |           |      |

## 3. Alternatives

[A bullet point list of any alternative approaches that were considered and why they were not chosen.]
- **ALT-001**: Alternative approach 1

## 4. Dependencies

[List any dependencies that need to be addressed, such as libraries, frameworks, or other components.]
- **DEP-001**: Dependency 1

## 5. Files

[List the files that will be affected by the feature or refactoring task.]
- **FILE-001**: Description of file 1

## 6. Testing

[List the comprehensive test suites or overarching test strategies that apply to the entire feature/plan.]
- **TEST-001**: Description of overarching test 1

## 7. Risks & Assumptions

[List any risks or assumptions related to the implementation of the plan.]
- **RISK-001**: Risk 1
- **ASSUMPTION-001**: Assumption 1

## 8. Related Specifications / Further Reading

[Link to related spec 1]
[Link to relevant external documentation]
```
