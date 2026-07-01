---
name: memory-manager
description: "Standardized workflow for discovering, reading, and writing the project's memory file (memory.instructions.md) to persist context across chat sessions."
license: MIT
---

<!-- markdownlint-disable -->

# Memory Manager Skill

## Overview

This skill provides a standardized protocol for managing the project's persistent memory file (`memory.instructions.md`). It ensures that AI agents can reliably save and restore context across chat sessions, regardless of which instruction directory the project uses. This skill is **agent-agnostic** — any agent in the ecosystem can invoke it.

## When to Use

- **Write Mode:** At the end of a significant milestone or phase completion, when the user agrees to save progress.
- **Read Mode:** At the start of a new chat session to bootstrap context from prior sessions.

---

## Workflow 1: File Discovery Protocol (Mandatory First Step)

> **⚠️ DIRECTIVE:** This workflow MUST be executed before ANY read or write operation. Never hardcode or assume the memory file path.

1. **Search recursively for `memory.instructions.md`** across ALL subdirectories within the project, prioritizing the following instruction roots and their subfolders:
   - `.omp/instructions/` (and subfolders)
   - `.pi/instructions/` (and subfolders)
   - `.commandcode/instructions/` (and subfolders)
   - `.opencode/instructions/` (and subfolders)
   - `.github/instructions/` (and subfolders)
   - `.agents/instructions/` (and subfolders)
   - `instructions/` (and subfolders at the project root)
2. **Use recursive search tools** (such as `grep_search` searching for filename `memory.instructions.md` or glob patterns like `**/memory.instructions.md`) to scan across subfolders, ignoring build/vendor folders (`node_modules`, `.git`, `dist`).
3. **Resolution:**
   - **If exactly ONE file is FOUND:** Lock the discovered path as the target for all subsequent read/write operations in this session.
   - **If MULTIPLE files are FOUND:** You MUST pause and present the list of found paths to the user. Ask the user which path should be locked as the active memory for this session. Do NOT proceed until the user explicitly chooses one.
   - **If NOT FOUND in any location:** Create the `instructions/` folder at the project root and initialize a new `memory.instructions.md` file inside it using the **Initial Memory Template** below.

### Initial Memory Template (For New Files Only)

```md
# Project Memory Log

> Active Location: [path_where_this_file_is_created]
> This file is managed by the `memory-manager` skill.
> It persists context across AI chat sessions to prevent knowledge loss.
> Do NOT manually edit this file unless necessary.

---
```

---

## Workflow 2: Read Mode (Context Bootstrap)

Use this workflow to load context at the beginning of a new session.

1. **Execute Workflow 1** to locate the memory file.
2. **Read the entire file** using the appropriate read tool.
3. **Extract and internalize** the following critical fields from the most recent checkpoint entry:
   - **Current SDLC Phase** — Which phase of the development lifecycle is active.
   - **Active Artifacts** — Status of key SDLC documents (PRD, Spec, Plan).
   - **Latest Milestones** — What was accomplished in the last session(s).
   - **Dead-Ends** — Approaches that failed previously. Do NOT repeat these.
   - **Pending Actions / Blockers** — What remains to be done or what issues are unresolved.
   - **Checkpoint Tail** — The 1-sentence HTML comment at the bottom for rapid context recovery.
4. **Acknowledge to the user** (in Bahasa Indonesia) that context has been loaded AND explicitly state the locked path. Example:
   > _"Saya telah membaca memori proyek dari `[discovered_path]`. Fase SDLC terakhir adalah [Phase]. Progres terakhir mencakup [Milestones]. Saya siap melanjutkan."_
5. **Proceed** with the user's request, now fully informed by historical context.

---

## Workflow 3: Write Mode (Context Checkpoint)

Use this workflow to persist progress after a significant milestone.

1. **Execute Workflow 1** to locate the memory file.
2. **Synthesize** the current session's achievements. Do NOT copy-paste raw conversation. Summarize concisely:
   - What phase was completed or advanced.
   - What documents or files were created/modified.
   - What decisions were made.
   - What remains to be done next.
3. **Append** a new checkpoint entry to the **bottom** of the memory file using the **Mandatory Checkpoint Template** below. Do NOT overwrite or delete existing entries unless the user explicitly requests a memory compaction.
4. **Confirm to the user** (in Bahasa Indonesia) that the checkpoint has been saved AND explicitly state the locked path. Example:
   > _"Checkpoint memori telah disimpan ke dalam `[discovered_path]`. Progres sesi ini telah dicatat untuk kontinuitas di sesi berikutnya."_

### Mandatory Checkpoint Template

```md
## 📝 Session Checkpoint: [YYYY-MM-DD]

- **Active Memory Path:** [path_to_this_file]
- **Current SDLC Phase:** [e.g., Planning / Specification / Implementation / Review / Documentation]
- **Active Artifacts:**
  - `[path/to/prd-feature-*.md]` — Status: ✅ Finalized
  - `[path/to/spec.md]` — Status: 🔄 In Progress
  - `[path/to/plan.md]` — Status: ⏳ Pending
- **Achieved Milestones:**
  - [Concise description of what was accomplished]
  - [Another achievement, if any]
- **Dead-Ends (Do NOT Repeat):**
  - **Attempted:** [Approach that was tried and failed]
  - **Reason:** [Why it failed / root cause]
- **Updated Files:**
  - `[relative/path/to/file1]` — [Brief description of change]
  - `[relative/path/to/file2]` — [Brief description of change]
- **Decisions Made:**
  - [Key architectural or design decision, if any]
- **Next Action / Pending:**
  - [What the next agent or session should pick up]
  - [Any unresolved blockers or open questions]

<!-- checkpoint-tail: [1-sentence summary for rapid context recovery by AI at session start] -->

---
```

---

## Anti-Patterns (What to Avoid)

- **Hardcoding paths:** Never assume the memory file is always in `.opencode/instructions/`. Always run the Discovery Protocol first.
- **Dumping raw logs:** The checkpoint must be a synthesis, not a transcript. Keep entries concise and actionable.
- **Overwriting history:** Always append new checkpoints. Never delete old entries unless the user explicitly asks for memory compaction.
- **Skipping acknowledgment:** Always confirm to the user that the read or write operation was successful.
