---
name: artifact-consistency-checker
description: "Performs consistency and traceability audits across documents (PRD vs Spec vs Plan) to detect missing coverage and scope creep."
license: MIT
---
<!-- markdownlint-disable -->
# Artifact Consistency Checker Skill

## Overview

This skill focuses on verifying the **traceability** and **consistency** of your Software Development Life Cycle (SDLC) artifacts. It is used to ensure that no single *requirement* is missed, and no "dark features" are added without justification when moving from the PRD document, to the Technical Specification, and finally to the Implementation Plan. This skill accompanies the `@ArtifactConsistencyChecker` agent.

## When to Use

Use this skill when:
- The user has finished creating the *Implementation Plan* and is ready to start *coding* (invoking `@GodModeDev`).
- The team suspects an indication of *scope creep* (features being added silently without business approval).
- There is confusion regarding which document is the latest *Source of Truth*.
- The user specifically requests an "audit", "consistency check", "traceability review", or "traceability matrix".

---

## Operational Workflow

### Phase 1: Artifact Aggregation
Collect all documents related to the current feature in progress. You **must** read and retain the context of at least TWO of the following documents to perform a comparison:
1. PRD (e.g., `prd-feature-*.md`) (Upstream Document / Business Needs)
2. `spec-*.md` (Middle Document / Architectural Specs)
3. `plan-*.md` (Downstream Document / Implementation Plan & Tasks)

### Phase 2: Tri-Directional Audit
Perform a rigorous point-by-point mapping:
- **Upstream to Downstream (Missing Coverage):** Take requirement X in the PRD, check if requirement X has an architectural design in the Spec, and has an explicit execution *task* in the Plan.
- **Downstream to Upstream (Orphaned Items):** Take *task* Y in the Plan, trace upwards (to Spec/PRD) to see who requested *task* Y. If no one requested it, this is *scope creep*.
- **Lateral (Contradictions):** Look for specific parameters (file size limits, time limits, SLAs, frameworks) and ensure the numbers are consistent and do not contradict each other across all documents.

### Phase 3: Reporting & Corrective Action
Create an audit report using the *Consistency Audit Report* format. If the audit status is **FAIL** or there are major issues, **deny** the user permission to proceed to the next phase. The user must align and correct the faulty documents first.

---

## Consistency Quality Standards

### Detecting Scope Creep (Orphaned Items)

Look for technical tasks that are excessive and have no foundation or were never requested by business documents.

```diff
# Example in Plan (BAD)
- Setup a Kubernetes cluster with 3 nodes for auto-scaling.
- Setup a separate Redis Cluster for caching search responses.

# Challenge/Audit (GOOD)
+ Did the PRD request this level of performance and scalability? The PRD only states "Internal app for a maximum of 5 concurrent users".
+ Therefore, Kubernetes and Redis are Orphaned Items (potential Over-engineering).
```

### Detecting Missing Coverage

Look for sweet promises in the PRD that are never technically executed in the *planning* stage.

```diff
# Example in PRD (Upstream)
- Users must receive an email notification immediately when their PDF file finishes compressing.

# Example in Plan (Downstream) (BAD)
- 1. Create upload UI page
- 2. Implement compression using PDF.js module
- 3. Provide a download button at the end of the process

# Challenge/Audit (GOOD)
+ The email sending feature (e.g., SMTP integration) is completely missing in the Plan. This is Missing Coverage!
```

---

## Implementation Guidelines

### DO (Always)
- **Enforce Traceability:** Whenever you validate a *Plan*, ensure you can point exactly to the sentence or ID in the PRD/Spec that justifies the task.
- **Block (Halt) the Coding Process:** Apply a *halt* status on development if the documents are still fundamentally contradictory.

### DON'T (Avoid)
- **Subjectively Evaluating Architecture Quality:** Do not complain if the user plans to use *React* instead of *Vue*, UNLESS the PRD/Spec documents specifically forbid it. Your focus is strictly "Are these documents aligned?".
- **Auto-Fix (Fixing it yourself):** Do not unilaterally modify and overwrite PRD or Plan documents to force content alignment without user approval. You cannot know for sure which document (Upstream or Downstream) represents the user's true intention.
