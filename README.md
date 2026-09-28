# ⚡ Personal Agentic Method (Ultra-Lightweight + Continuous Memory)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Zero Dependency](https://img.shields.io/badge/Dependencies-0%20(Pure%20Markdown)-brightgreen.svg)](#)
[![Size](https://img.shields.io/badge/Size-%3C%2030KB-orange.svg)](#)
[![Methodology](https://img.shields.io/badge/Methodology-Agile%204--Step%20Loop-purple.svg)](#)
[![Domains](https://img.shields.io/badge/Domains-Code%20%7C%20Writing%20%7C%20Research%20%7C%20Data-blueviolet.svg)](#)

An ultra-lightweight, personal Agile framework for collaborating with **AI Assistants & Autonomous Agents** across **Software Engineering, Writing, Academic Research, Data Analysis, and Knowledge Work** (Google Antigravity IDE, Claude Code, Cursor, Windsurf, ChatGPT, Gemini, GitHub Copilot, etc.).

Distilled from the core principles of [BMad Method](https://github.com/bmad-code-org/BMAD-METHOD), stripping away 1,500+ cumbersome files and heavy npm dependencies: **0 installations, 0 runtime dependencies, < 30KB total footprint**.

Featuring built-in **Session Continuity** and **Self-Learning (Anti-Pattern Memory)** so your AI:
1. 🧠 **Never suffers from session amnesia** when you start a new chat session.
2. 🛡️ **Never repeats past mistakes** by reading from an evolving immune system of learned patterns.
3. 🎯 **Never produces sloppy or unrequested output** through strict "one task at a time" discipline.

---

## 🌍 Versatile Across Any Domain (Not Just Coding!)

While born from agile engineering workflows, the Personal Agentic Method is a **domain-agnostic cognitive collaboration operating system**. Any complex knowledge work benefits immediately:

| Domain | What `spec.md` defines | What `tasks.md` tracks | What `learned-patterns.md` remembers |
|---|---|---|---|
| 💻 **Software Engineering** | Architecture, APIs, In/Out Scope | Step-by-step modular code execution | Library gotchas, anti-patterns, framework traps |
| ✍️ **Content & Marketing** | Campaign briefs, target persona, Tone of Voice | Outline ➔ Hook ➔ Draft ➔ Visuals ➔ Review | Clichés to avoid, high-converting hook formulas |
| 🔬 **Research & Writing** | Research questions, methodology, thesis outline | Literature review ➔ Data synthesis ➔ Chapters | APA/IEEE citation standards, debunked sources |
| 📊 **Data & Analytics** | Business problems, hypotheses, metric definitions | Data cleaning ➔ EDA ➔ Modeling ➔ Insights | Company churn formulas, executive visual styles |
| 📋 **Product & Ops** | Product PRDs, Standard Operating Procedures (SOP) | Milestone roadmap, weekly rollout checklist | Ambiguous interview prompts, payroll pitfalls |

---

## 📁 Repository Structure

```
agentic-method-light/
├── .gitignore
├── LICENSE                     # MIT License
├── AGENTS.md                   # Operational guidelines & behavioral rules for AI
├── templates/                  # Ready-to-use template suite
│   ├── spec.md                 # Specification, scope & acceptance criteria template
│   ├── tasks.md                # Actionable task checklist template
│   ├── notes.md                # Strategic decisions, ADRs & environment notes
│   ├── learned-patterns.md     # Knowledge base of past errors & enforced standards
│   └── work-logs/              # Date-partitioned session handoff logs
│       └── init.md             # Seed work log template
└── README.md                   # Documentation & setup guide
```

---

## 🧠 How Continuous Memory & Learning Work

### 1. The `artifacts/work-logs/` Directory (Preventing Session Amnesia)
- Each time a task is completed or when ending a session, the AI automatically creates a date-based directory:  
  `artifacts/work-logs/YYYY-MM-DD/` (e.g., `artifacts/work-logs/2026-09-28/`).
- Inside that directory, the AI records a concise handoff log:  
  `artifacts/work-logs/YYYY-MM-DD/<task-name>.md` (or `HHmm-<task-name>.md` if multiple tasks occur in a single day).
- Every log captures 4 essential points:
  1. **Completed**: What was accomplished.
  2. **Changed Files**: Modified and created files.
  3. **Current Checkpoint**: Exactly where work was paused.
  4. **Next Step**: The immediate first action to take in the next session.
- **Starting a new chat**: The AI locates the **latest date directory** and reads the **newest log file** to immediately restore full context—saving 80–90% of prompt tokens without loading old, noisy chat history.

### 2. The `artifacts/learned-patterns.md` File (Immune System Against Errors)
- Whenever a tricky bug, logical flaw, or misconception is resolved, or whenever you correct the AI's approach, the AI proactively logs a new entry:
  - *Context & Encountered Issue*
  - *WRONG Approach (Forbidden to repeat)*
  - *CORRECT Approach (Enforced project standard)*
  - *Scope / Module*
- At the start of every session, the AI reads this file to "vaccinate" itself against past mistakes.

---

## 🚀 Setup & Integration Guide

You can integrate Personal Agentic Method into any project using any of the following approaches:

### Option 1: Fast Terminal Helper (Recommended)

1. Clone this repository to your local machine (e.g., to `~/agentic-method-light`):
   ```bash
   git clone https://github.com/tkstung104/agentic-method-light.git ~/agentic-method-light
   ```

2. Add the following helper function to your shell configuration (`~/.bashrc` or `~/.zshrc`):
   ```bash
   init-agentic() {
       local target="${1:-.}"
       local source_dir="$HOME/agentic-method-light"
       local today
       today=$(date +%Y-%m-%d)

       if [ ! -d "$source_dir" ]; then
           echo "❌ Directory $source_dir not found. Please clone the repository first!"
           return 1
       fi

       echo "🚀 Applying Personal Agentic Method to: $target"
       mkdir -p "$target/artifacts/work-logs/$today"

       # Copy AGENTS.md
       [ ! -f "$target/AGENTS.md" ] && cp "$source_dir/AGENTS.md" "$target/AGENTS.md" && echo "  ✓ AGENTS.md"

       # Copy templates into artifacts
       for file in spec.md tasks.md notes.md learned-patterns.md; do
           [ ! -f "$target/artifacts/$file" ] && cp "$source_dir/templates/$file" "$target/artifacts/$file" && echo "  ✓ artifacts/$file"
       done

       # Copy seed work-log into today's folder
       [ ! -f "$target/artifacts/work-logs/$today/init.md" ] && cp "$source_dir/templates/work-logs/init.md" "$target/artifacts/work-logs/$today/init.md" && echo "  ✓ artifacts/work-logs/$today/init.md"

       echo "🎉 Initialized! You can now collaborate with your AI using the 4-step loop."
   }
   ```

3. Reload your shell (`source ~/.bashrc` or `source ~/.zshrc`).  
   From now on, whenever you navigate to any project folder, simply run **a single command**:
   ```bash
   cd /path/to/my-project
   init-agentic
   ```
   The entire `AGENTS.md` and `artifacts/` hierarchy will be provisioned in **0.1 seconds**!

---

### Option 2: Manual Copy (Zero Shell Config)

If you only want to apply this to a single project without shell helpers:
```bash
# From within your target project directory:
TODAY=$(date +%Y-%m-%d)
cp /path/to/agentic-method-light/AGENTS.md ./
mkdir -p "artifacts/work-logs/$TODAY"
cp /path/to/agentic-method-light/templates/*.md ./artifacts/
cp /path/to/agentic-method-light/templates/work-logs/init.md "./artifacts/work-logs/$TODAY/init.md"
```

---

### Option 3: Global Rules for AI Assistants & IDEs

You can embed `AGENTS.md` directly into your global AI assistant configurations:

- **Google Antigravity IDE**:
  ```bash
  mkdir -p ~/.gemini/config/rules/
  cp /path/to/agentic-method-light/AGENTS.md ~/.gemini/config/rules/personal-agentic.md
  ```
- **Cursor**: Copy the contents of `AGENTS.md` into **Rules for AI** in User Settings or place it into `.cursorrules` in your project root.
- **Claude Code**: Embed or rename `AGENTS.md` as `CLAUDE.md` in your project root.
- **Windsurf / GitHub Copilot**: Add the contents of `AGENTS.md` into Global System Instructions or `.github/copilot-instructions.md`.
- **ChatGPT / Claude Web**: Paste the contents of `AGENTS.md` into Custom Instructions or Project Knowledge.

---

## 🔄 The 4-Step Agile Loop in Practice

```
[Session Start] AI reads latest work-logs/ + learned-patterns.md + tasks.md
  │
  ▼
[Step 1: Spec] AI asks 1-3 clarifying questions ──► Writes to artifacts/spec.md
  │
  ▼
[Step 2: Plan] AI decomposes tasks sequentially ─► Writes checklist to artifacts/tasks.md
  │
  ▼
[Step 3: Implement] AI executes STRICTLY 1 TASK ──► Marks [x] in artifacts/tasks.md
  │
  ▼
[Step 4: Verify] AI checks criteria & quality ────► Records lessons to learned-patterns.md
  │                                            └──► Saves new handoff log to work-logs/
  ▼
[Pause or Proceed to Next Task]
```

### ⚡ Handling Mid-Flight Scope Changes
If you change direction, adjust requirements, or add features while work is in progress:
- The AI **must halt execution immediately** without unauthorized work.
- Return to **Step 1** to update `spec.md` and **Step 2** to revise `tasks.md`.
- Present the delta to you and await confirmation before resuming execution.

---

## 📂 The `artifacts/` Directory (Single Source of Truth)

| File / Directory | Purpose |
|---|---|
| `artifacts/spec.md` | Problem definition, scope boundaries (In/Out-of-Scope), user journeys, and acceptance criteria. |
| `artifacts/tasks.md` | Actionable task checklist organized by implementation phases. |
| `artifacts/work-logs/` | Date-partitioned session logs (`YYYY-MM-DD/<task>.md`) enabling seamless handoffs across chat sessions. |
| `artifacts/learned-patterns.md` | Living knowledge base of resolved issues, gotchas, conventions, and mandatory standards. |
| `artifacts/notes.md` | Lightweight strategic notes, environment variables, Architecture Decision Records (ADRs). |

> [!TIP]
> **Version Control Best Practice**: Always commit the `artifacts/` directory along with your project source files. If your project's `.gitignore` ignores `artifacts/`, add an exception (`!artifacts/`) to preserve project memory in version control.

---

## 📜 License

Distributed under the [MIT License](LICENSE). Free for both personal and commercial use.
