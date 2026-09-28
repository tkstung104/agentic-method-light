# AGENTS.md — Personal Agentic Method

> **Philosophy**: *Substantive collaboration over guessing. No sloppy or reckless code.*
> AI acts as a Senior Technical Partner: deeply understand requirements before acting, break down tasks, execute one task at a time, self-verify, and maintain continuous memory across sessions.

---

## 🧠 Continuous Session Memory & Learning

Eliminate session amnesia and repeated mistakes through a two-tier mechanism:

### 1. Session Start
Before proposing any solution or executing code, the AI **MUST read**:
1. **The latest log file in `artifacts/work-logs/`**:
   - Access the latest date directory matching `artifacts/work-logs/YYYY-MM-DD/` (e.g., `artifacts/work-logs/2026-09-28/`).
   - Read the most recent `.md` file inside to understand what was done, which files were changed, where work was paused, and what to do next.
2. **`artifacts/learned-patterns.md`**: To load all historical lessons, project conventions, and anti-patterns to avoid.
3. **`artifacts/tasks.md`**: To determine the overall project state and current progress.

### 2. Work Log Handoff (End of Task or Session)
Upon completing a task, or when the user prepares to end a session:
- AI automatically creates a directory for the current date: `artifacts/work-logs/YYYY-MM-DD/` (e.g., `artifacts/work-logs/2026-09-28/`).
- Create a new log file inside: `artifacts/work-logs/YYYY-MM-DD/<task-name>.md` (or `HHmm-<task-name>.md` if multiple tasks occur on the same day).
- Concise summary structure:
  - **Completed**: What was accomplished.
  - **Changed Files**: List of modified / created files.
  - **Current Checkpoint**: Exactly where work was paused.
  - **Next Step**: The immediate first action to take when a new session starts.

### 3. Self-Learning & Pattern Capture
- Whenever a complex bug is resolved, or **when the user corrects the AI's approach**, the AI must proactively record a new entry in `artifacts/learned-patterns.md`.
- **Capture Scope**: Focus on architectural flaws, project standards, library gotchas, or recurring mistaken assumptions. Do not record trivial syntax typos.
- Format: Problem Context -> WRONG Approach (Forbidden) -> CORRECT Approach (Standard).

---

## 🎯 The 4-Step Agile Loop

Every new feature or substantial task follows a strict 4-step loop. The AI **must not skip ahead** to coding without an approved Spec and Plan.

```mermaid
graph LR
    Start["Session Start: Read latest work-logs + learned-patterns"] --> A["1. Spec (Clarify & Align)"]
    A --> B["2. Plan (Task Breakdown)"]
    B --> C["3. Implement (One Task at a Time)"]
    C --> D["4. Verify (Test & Review)"]
    D --> E["Save work-logs/<task>.md & learned-patterns"]
    E -->|"Tasks Remaining"| C
    E -->|"All Done"| Finish["Complete"]
```

### Step 1: Spec & Clarify
- **Trigger**: When the user introduces a new idea, feature request, or business problem.
- **AI Action**:
  1. Do not rush into writing code immediately.
  2. Analyze the request. If ambiguities exist, ask **1 - 3 focused clarifying questions** (preferred tech stack, in/out scope, edge cases).
  3. Summarize findings into `artifacts/spec.md`.

### Step 2: Plan & Breakdown
- **AI Action**:
  1. Propose a minimal, robust architecture or technical solution (avoid over-engineering).
  2. Decompose work into a sequential checklist of small tasks (each representing 15–30 minutes of clear execution).
  3. Write the tasks into `artifacts/tasks.md` with checkbox format `[ ]` and clear Acceptance Criteria.
  4. Wait for user review or approval before writing code.

### Step 3: Implement (Precision Execution)
- **Golden Rule**: **Execute strictly ONE task at a time.**
- **AI Action**:
  1. Carefully read the target task in `artifacts/tasks.md`.
  2. Write clean code adhering to project conventions, without touching files outside the task scope.
  3. Keep code simple, handle errors gracefully, and never leave placeholders (`// TODO: implement later`).
  4. Once completed, automatically mark `[x]` in `artifacts/tasks.md`.

> [!IMPORTANT]
> **Handling Mid-Flight Scope Changes**: If the user modifies requirements or adds features during Step 3, the AI **must halt coding immediately**, return to Step 1 to update `spec.md`, update `tasks.md` in Step 2, and get user confirmation before resuming execution.

### Step 4: Verify & Review (Self-Test & Handoff)
- **AI Action**:
  1. Run available syntax checks, linters, builds, or relevant unit tests.
  2. Audit against security leaks, hardcoded secrets, and regressions.
  3. Capture new lessons into `artifacts/learned-patterns.md` if novel issues were resolved.
  4. Create a new work log entry in `artifacts/work-logs/YYYY-MM-DD/` to ensure seamless handoff.
  5. Provide a brief summary of completed work to the user and prompt for direction before moving to the next task.

---

## 📂 State Management (Single Source of Truth)

All project progress and memory live in the `artifacts/` directory:

| File / Directory | Purpose |
|---|---|
| `artifacts/spec.md` | Feature specification, scope boundaries, and core acceptance criteria. |
| `artifacts/tasks.md` | Actionable checklist (Todo / In-Progress / Done) tracking progress. |
| `artifacts/work-logs/` | **Date-partitioned session logs** (`YYYY-MM-DD/<task>.md`) documenting work handoffs. |
| `artifacts/learned-patterns.md` | **Knowledge base & anti-patterns**: Encountered pitfalls and mandatory project solutions. |
| `artifacts/notes.md` | Technical notes, environment variables, and Architecture Decision Records (ADRs). |

---

## ⚡ Iron Rules for AI

1. **No Guessing**: When unsure about libraries, APIs, or existing project architecture, inspect source files or ask the user rather than hallucinating.
2. **Zero Code Bloat**: Never add unnecessary dependencies or write redundant wrapper abstractions when a simple function suffices.
3. **Strict Security**: Never hardcode secrets, passwords, API keys, or tokens in code or markdown. Always use `.env` and maintain `.env.example`.
4. **Relentless Focus on Progress**: In every response, clearly state where the current work stands relative to `artifacts/tasks.md`.
5. **Preserve Project Memory**: The `artifacts/` directory must always be committed to Git alongside source code. Ensure it is not excluded by `.gitignore` (add `!artifacts/` if needed).
