---
name: product-manager-prd
description: "Workflow to generate a comprehensive Product Requirements Document (PRD) detailing user stories, acceptance criteria, technical considerations, and metrics."
license: MIT
---
<!-- markdownlint-disable -->
# Product Manager PRD Skill

## Overview
This skill outlines the workflow to define the **WHY, WHO, and WHAT** from the user and business perspective. It translates business goals into actionable requirements and user stories, saving the output as `prd-feature-<feature_name>-<date_ddmmyyyy>.md`. This skill accompanies the `@ProductManagerPRD` agent.

## When to Use
- When initiating a new project or major feature.
- When you need to translate business requirements into structured User Stories and Acceptance Criteria.

---

## PRD Generation Workflow

1.  **Analyze Context:** Review the existing codebase only to understand Technical Constraints and Integration Points that might affect the PRD.
2.  **Clarification Protocol:** Ask 3-5 questions to better understand the user's needs, focusing on the WHY and WHO before the WHAT.
3.  **Structure the Document:** Organize the PRD strictly according to the `Mandatory PRD Template` below.
4.  **Write User Stories:** Use the Agile format: *"As a [type of user], I want to [goal], so that [reason]."* Assign a unique ID (e.g., `GH-001`).
5.  **Define Acceptance Criteria:** List specific SMART criteria with a checklist format (`- [ ]`).
6.  **File Creation:** Save the file using the format `prd-feature-<feature_name>-<date_ddmmyyyy>.md` (e.g., `prd-feature-login-system-08062026.md`).
7.  **Issue Creation:** After presenting the PRD, proactively ask if the user would like to create GitHub issues for the user stories. If they agree, output the terminal commands to create them or create them via API.

---

## Mandatory PRD Template

```md
## PRD: {project_title}

## 1. Product overview
### 1.1 Document title and version
- PRD: {project_title}
- Version: {version_number}

### 1.2 Product summary
- Brief overview (2-3 short paragraphs).

## 2. Goals
### 2.1 Business goals
- Bullet list.
### 2.2 User goals
- Bullet list.
### 2.3 Non-goals (Out of Scope)
- Bullet list.

## 3. User personas
### 3.1 Key user types
- Bullet list.
### 3.2 Basic persona details
- **{persona_name}**: {description}
### 3.3 Role-based access
- **{role_name}**: {permissions/description}

## 4. Functional requirements
- **{feature_name}** (Priority: {priority_level})
  - Specific requirements for the feature.

## 5. User experience
### 5.1 Entry points & first-time user flow
- Bullet list.
### 5.2 Core experience
- **{step_name}**: {description}
### 5.3 UI/UX highlights & Edge cases
- Bullet list.

## 6. Narrative
Concise paragraph describing the user's journey and benefits.

## 7. Success metrics
### 7.1 User-centric metrics
- Bullet list.
### 7.2 Business metrics
- Bullet list.
### 7.3 Technical metrics
- Bullet list.

## 8. Technical considerations (Input for Engineering Team)
### 8.1 Integration points
- Bullet list.
### 8.2 Data storage & privacy
- Bullet list.
### 8.3 Scalability & potential technical challenges
- Bullet list.

## 9. Milestones & sequencing
### 9.1 Project estimate & Team composition
- {Size}: {time_estimate} | {Team}: {roles involved}
### 9.2 Suggested phases
- **{Phase number}**: {description} ({time_estimate})

## 10. User stories & Acceptance Criteria

### 10.1. {User story title}
- **ID**: {GH-001}
- **Story**: As a [type of user], I want to [goal], so that [reason].
- **Acceptance criteria**:
  - [ ] {SMART Criteria 1}
  - [ ] {SMART Criteria 2}
```
