---
name: diataxis-documentation-architect
description: "Workflow for auditing, designing, and writing structured documentation based on the Diátaxis Framework (Tutorials, How-to, Reference, Explanation)."
license: MIT
---
<!-- markdownlint-disable -->
# Diátaxis Documentation Architect Skill

## Overview
This skill outlines the workflow to design documentation architecture and create high-quality documentation strictly adhering to the **Diátaxis Framework**. It ensures every piece of documentation serves one specific purpose and does not mix modes. This skill accompanies the `@DiataxisDocumentationArchitect` agent.

## When to Use
- When creating user-facing or developer-facing documentation.
- When generating tutorials, how-to guides, reference material, or conceptual explanations.

---

## 🧭 The 4 Quadrants (Strict Rules)

### 1. 🎓 TUTORIALS (Learning-oriented)
- **Goal:** Allow the beginner to learn by doing a specific project.
- **Characteristics:** Instructional, step-by-step, builds understanding incrementally. Assumes no prior knowledge.
- **Voice:** Second person ("You"). Encouraging and prescriptive.
- **Rule:** NO abstract theory. NO choices/alternatives. Just "do this, then do that."

### 2. 🛠️ HOW-TO GUIDES (Task-oriented)
- **Goal:** Solve a specific problem or complete a task.
- **Characteristics:** A recipe. Series of steps to achieve a concrete result. Assumes some familiarity.
- **Voice:** Second person ("You"). Direct and action-oriented.
- **Rule:** NO teaching "basic concepts". Get straight to the solution.

### 3. 📖 REFERENCE (Information-oriented)
- **Goal:** Provide factual description of components.
- **Characteristics:** Concise, exhaustive. API specs, class descriptions, parameter lists.
- **Voice:** Third person or passive voice. Technical, dry, and austere.
- **Rule:** NO instructional steps. Just facts. Map the code 1:1 to text.

### 4. 💡 EXPLANATION (Understanding-oriented)
- **Goal:** Deepen understanding and clarify context, background, and "Why".
- **Characteristics:** Discursive, contextual. Discusses design decisions, trade-offs, and concepts.
- **Voice:** Engaging narrative.
- **Rule:** NO code snippets (unless for illustration). NO instructions.

---

## ⚙️ Operational Workflow

Follow this process sequentially:

### Phase 1: Audit & Clarify
1. **Analyze Request:** Determine the target audience, the project's maturity, and existing materials.
2. **Clarification Checkpoint:** If the request is too broad, ask the user which specific component or quadrant to focus on first. **MUST ask whether they prefer Markdown (`.md`) or Plain Text (`.txt`).**
3. **Scan Codebase:** Use search/read tools to look at the actual code, functions, or APIs.

### Phase 2: Design & Outline
1. **Propose Strategy:** Tell the user: *"I recommend writing a **[Quadrant Name]** document to achieve this."*
2. **Outline:** Create a bulleted outline of the document structure tailored to the specific quadrant.
3. **Wait for Approval:** Do not write the full document until the user approves the outline.

### Phase 3: Drafting & File Creation
1. Write the content in clear, professional formatting (in Bahasa Indonesia by default).
2. **Verify Code:** Ensure every code snippet in the docs matches the actual codebase logic perfectly.
3. **File Management:** Save the document to a logically categorized folder (e.g., `/docs/tutorials/`, `/docs/reference/`).

---

## 🛑 Anti-Patterns (What to Avoid)
- **The "All-in-One" Trap:** Do not write a document that tries to teach a concept AND list every API parameter AND show a tutorial. Split them up into separate files.
- **Assuming Knowledge:** In Tutorials, assume zero knowledge. In How-Tos, assume basic competence.
- **Outdated Info:** Always verify facts against the current codebase results.
