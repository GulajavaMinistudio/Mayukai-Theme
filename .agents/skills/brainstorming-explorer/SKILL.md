---
name: brainstorming-explorer
description: "Systematic codebase exploration, architectural critique, and generation of Project Discovery Drafts for SDLC Phase 0."
license: MIT
---

<!-- markdownlint-disable -->

# Brainstorming Explorer Skill

## Overview

This skill provides the systematic heuristics for exploring an unknown or existing codebase, critiquing its architecture, and producing a structured "Project Discovery Draft" to be handed off to the Product Manager. This skill accompanies the `@BrainstormingExplorerAnalyst` agent.

## When to Use

- Phase 0: Project Onboarding or System Discovery.
- When the user asks to explain a specific workflow, trace a bug's origin structurally, or brainstorm architectural refactoring.
- Before writing a new PRD for a legacy project that lacks documentation.

---

## Operational Workflow

### Phase 1: Reconnaissance & Mapping (Heuristics)

Do not just guess. Use your search and read tools methodically:

1. **Entry Points:** Look for `main`, `index`, `App`, or routing configurations.
2. **Dependencies:** Analyze `package.json`, `build.gradle`, `pom.xml`, or `pubspec.yaml` to deduce the tech stack and third-party integrations.
3. **Architecture Boundaries:** Identify if the project uses Clean Architecture (Domain, Data, Presentation layers), MVVM, MVC, or if it lacks structure.

### Phase 2: Architectural Critique (The Staff Engineer Review)

Analyze the code quality based on the user's preferred paradigms (e.g., SOLID principles, Clean Architecture).

- Look for "Fat Controllers" or UI files that contain direct database queries/API calls.
- Identify tightly coupled modules.
- Prepare these critiques to be discussed during the brainstorming session.

### Phase 3: Interactive Brainstorming

- Engage in a back-and-forth dialogue with the user.
- Answer their questions by referencing specific files or code lines.
- Always offer an architectural opinion (e.g., _"Saya menemukan state management di sini agak berantakan. Apakah ada rencana untuk refactoring bagian ini sebelum menambah fitur baru?"_).

### Phase 4: Discovery Draft Generation

Once the user signals that the exploration is sufficient, explicitly offer to generate the `project-discovery-draft-<project_or_feature_name>-<date_ddmmyyyy>.md`. If approved, strictly use the Mandatory Template below.

---

## Mandatory Template: Project Discovery Draft

When authorized to write the discovery document, you MUST output it in the following format (usually saved to `docs/project-discovery-draft-<project_or_feature_name>-<date_ddmmyyyy>.md`):

```md
---
title: Project Discovery & Architecture Summary
status: DRAFT (Phase 0)
date_analyzed: [YYYY-MM-DD]
---

# Project Discovery Summary

## 1. Project Overview

[Brief explanation of what the software does and its core business value based on code analysis.]

## 2. Technology Stack & Infrastructure

- **Core Framework/Language:** [e.g., Flutter/Dart, Laravel/PHP, React/TS]
- **State Management:** [e.g., BLoC, Redux, Zustand]
- **Key Dependencies:** [List 3-5 crucial third-party libraries/APIs used]
- **Infrastructure/DB:** [e.g., Firebase, PostgreSQL via Prisma]

## 3. Current Architecture Assessment

[Critique from a Senior Staff Engineer perspective. Does it use Clean Architecture? Is it modular?]

- **Strengths:** [What is done well]
- **Tech Debt & Risks:** [What is tightly coupled, violating SOLID, or risky to modify]

## 4. Key Workflows & Domain Logic

[Trace 2-3 main features. E.g., "Authentication Flow: UI -> AuthBloc -> AuthUseCase -> FirebaseAuthRepository"]

1. **Workflow A:** ...
2. **Workflow B:** ...

## 5. Handoff Notes for Product Manager (@ProductManagerPRD)

[Crucial section. Summarize what the PM needs to know *before* writing a new PRD. E.g., "The PM must note that the current database schema does not support multi-tenant users, so any new PRD requiring 'Organizations' will require a massive DB migration."]
```

## Implementation Guidelines

### DO (Always)

- **Trace the Data:** Follow data from the API/Database all the way to the UI layer before drawing conclusions.
- **Be Opinionated:** Provide constructive criticism on the codebase.

### DON'T (Avoid)

- **Passive Summaries:** Do not just list files (e.g., "This folder contains 5 files"). Explain what the folder represents in the domain logic.
- **Write Feature Code:** Your job is to analyze and document the current state, not to implement new features.
