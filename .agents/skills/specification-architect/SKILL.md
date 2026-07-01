---
name: specification-architect
description: "Generates or updates highly detailed, machine-readable technical specification documents in the /spec/ directory."
license: MIT
---

<!-- markdownlint-disable -->

# Specification Architect Skill

## Overview

This skill is used to translate Product Requirements Documents (PRDs) into structured, unambiguous Technical Specifications. It defines the "WHAT" of the technical constraints, data contracts, and acceptance criteria without writing source code. This skill accompanies the `@SpecificationArchitect` agent.

## When to Use

- When transitioning from PRD (or Clarification Phase) to Technical Design.
- When you need to define data contracts, interfaces, and architecture boundaries.
- When updating an existing technical specification based on new business requirements.

---

## Operational Workflow

### Phase 1: Understand, Clarify, & Read PRD

- Ask if there is an existing PRD. If yes, you **MUST** read and analyze it to extract business goals and user stories.
- Clarify if creating a new spec or updating an existing one.

### Phase 2: Investigate the Codebase

- Explore the existing codebase using search/read tools to understand current data structures, dependencies, and test coverage.

### Phase 3: Collaborate & Technical Grilling (Iterative)

- Discuss findings with the user using the "Grill With Docs" method. Draft the specification sections focusing on **WHAT** the system should do.
- **Halt and Iterate:** Ask **ONE** specific question at a time regarding data contracts, interfaces, or constraints. Wait for the user's decision before asking the next question.
- **Do the Heavy Lifting:** Present technical trade-offs. (e.g., "The PRD requires real-time updates. Based on our codebase, we can use (A) the existing WebSockets implementation, or (B) implement Server-Sent Events (SSE). I recommend (A) for consistency. Do you agree?").
- Ensure all requirements are testable and unambiguous before moving to Phase 4.

### Phase 4: Quality Control & File Generation

- **Evaluate Complexity:** Determine if the specification can be consolidated into a single file. **Consolidate whenever possible to minimize file overhead.**
- **Modular Escalation:** Only propose splitting into multiple files if the specification covers distinct functional modules or becomes too large.
- **Master Index (If applicable):** If split, create a `spec-index.md` that serves as the entry point and links to all related spec files.
- **File Generation:** Generate files in the `/spec/` directory using naming convention `spec-[purpose]-[name].md`.
- **Consistency Check:** Ensure all internal links between spec files are relative and valid.

---

## Handling Edge Cases

- **Non-existent Implementation:** Define the spec based on design intent BEFORE code is written.
- **Complex Systems:** Break them down into smaller components and specify each individually.
- **Updates:** Highlight changes and ensure backward compatibility is documented.
- **File Consolidation:** If a spec update involves a small, related feature, append it to the existing specification rather than creating a new file.

---

## Mandatory Specification Template

You MUST strictly adhere to this template for all new specification files:

```md
---
title: [Concise Title Describing the Specification's Focus]
version: [Optional: e.g., 1.0, Date]
date_created: [YYYY-MM-DD]
last_updated: [Optional: YYYY-MM-DD]
owner: [Optional: Team/Individual responsible for this spec]
tags: [Optional: List of relevant tags or categories]
---

# Introduction

[A short concise introduction to the specification and the goal it is intended to achieve.]

## 1. Purpose & Scope

[Provide a clear, concise description of the specification's purpose and the scope of its application. State the intended audience and any assumptions.]

## 2. Definitions

[List and define all acronyms, abbreviations, and domain-specific terms used in this specification.]

## 3. Requirements, Constraints & Guidelines

[Explicitly list all requirements, constraints, rules, and guidelines. Use bullet points or tables for clarity.]

- **REQ-001**: Requirement 1
- **SEC-001**: Security Requirement 1
- **CON-001**: Constraint 1
- **GUD-001**: Guideline 1

## 4. Interfaces & Data Contracts

[Describe the interfaces, APIs, data contracts, or integration points. Use tables or code blocks for schemas and examples.]

## 5. Acceptance Criteria

[Define clear, testable acceptance criteria for each requirement using Given-When-Then format where appropriate.]

- **AC-001**: Given [context], When [action], Then [expected outcome]
- **AC-002**: The system shall [specific behavior] when [condition]

## 6. Test Automation Strategy

[Define the testing approach, frameworks, and automation requirements.]

- **Test Levels**: Unit, Integration, End-to-End
- **Test Data Management**: [approach for test data creation and cleanup]
- **CI/CD Integration**: [automated testing pipelines]
- **Coverage Requirements**: [minimum code coverage thresholds]

## 7. Rationale, Context & Architecture Decisions (ADRs)

[Explain the reasoning behind the requirements, constraints, and guidelines. If a "hard-to-reverse" architectural decision was made during the planning phase (e.g., choosing a specific database or protocol), document it here as an ADR (Context, Decision, Consequences).]

## 8. Dependencies & External Integrations

[Define the external systems, services, and architectural dependencies required. Focus on **what** is needed rather than **how** it's implemented.]

### External Systems

- **EXT-001**: [External system name] - [Purpose and integration type]

### Third-Party Services

- **SVC-001**: [Service name] - [Required capabilities and SLA requirements]

### Infrastructure Dependencies

- **INF-001**: [Infrastructure component] - [Requirements and constraints]

### Data Dependencies

- **DAT-001**: [External data source] - [Format, frequency, and access requirements]

## 9. Examples & Edge Cases

` ` `javascript
// Code snippet or data example demonstrating the correct application of the guidelines, including edge cases
` ` `

## 10. Validation Criteria

[List the criteria or tests that must be satisfied for compliance with this specification.]

## 11. Related Specifications / Further Reading

[Link to related spec 1]
[Link to relevant external documentation]
```

---

## Implementation Guidelines

### DO (Always)

- **Anchor to the Codebase:** Always reference existing patterns, libraries, or files in the current codebase when proposing technical options.
- **Identify ADRs:** Proactively point out when a user's choice is a "hard-to-reverse" architectural decision.

### DON'T (Avoid)

- **Machine Gun Questioning:** Do not ask multiple architectural questions in a single prompt. Resolve one interface/contract before moving to the next.
- **Silent Assumptions:** Do not automatically pick a data type, API protocol (REST/GraphQL), or library without verifying it with the user first.
