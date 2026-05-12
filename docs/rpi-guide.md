# RPI Guide — Research, Plan, Implement, Review

After completing the Design Thinking workshop, the next step is the **RPI (Research → Plan → Implement → Review)** workflow from [HVE Core](https://github.com/microsoft/hve-core). RPI transforms your validated DT outputs into working software.

---

## What Is RPI?

RPI is a four-phase structured workflow that prevents the most common AI-assisted coding failure: implementing before fully understanding the problem. Each phase is handled by a specialized HVE Core agent:

```
┌─────────────────────────────────────────────────────────────────┐
│   DT OUTPUTS  →  RPI WORKFLOW  →  WORKING SOFTWARE              │
│                                                                 │
│  DT Handoff Contract      ┌────────────────────────┐           │
│  (from /dt-handoff-        │  Phase 1: RESEARCH     │           │
│   implementation-space)   │  Task Researcher        │           │
│                           │  → research.md          │           │
│                           ├────────────────────────┤           │
│                           │  Phase 2: PLAN          │           │
│                           │  Task Planner           │           │
│                           │  → plan.md + details.md │           │
│                           ├────────────────────────┤           │
│                           │  Phase 3: IMPLEMENT     │           │
│                           │  Task Implementor       │           │
│                           │  → working code         │           │
│                           │  → changes.md           │           │
│                           ├────────────────────────┤           │
│                           │  Phase 4: REVIEW        │           │
│                           │  Task Reviewer          │           │
│                           │  → review.md            │           │
│                           └────────────────────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

> **Why this order matters:** AI coding assistants conflate investigation and implementation. RPI separates them by constraint: Task Researcher knows it cannot write code; this constraint forces it to verify before recommending. Task Planner knows it cannot implement; this forces complete planning before a single line is written.

---

## Prerequisites

- HVE Core All installed: `code --install-extension ise-hve-essentials.hve-core-all`
- Design Thinking workshop complete through Method 9 (or at least the Problem Space and Solution Space)
- DT Handoff Contract created by running `/dt-handoff-implementation-space` in Copilot Chat

---

## Step 1: Generate the DT Handoff Contract

In Copilot Chat, with DT Coach active:

```
/dt-handoff-implementation-space
```

This runs the `dt-rpi-handoff-contract` instruction, which converts your DT artifacts into an RPI work contract. The output is stored in `.copilot-tracking/dt/{project-slug}/`, where `{project-slug}` is the kebab-case identifier you used when starting the project (e.g., `sponsor-discount-reconciliation`). It captures:

- Validated user needs (from Methods 1–3)
- Chosen solution concept (from Methods 5–6)
- Acceptance criteria (from Methods 7–8)
- Known constraints and non-goals

Review this contract before proceeding — it is the input specification for all RPI phases.

---

## Step 2: Research

```
/task-research <topic>
```

Alternatively, select **Task Researcher** from the agent picker and describe your task.

### What to research

Provide the DT handoff contract as context and ask Task Researcher to investigate:

```
I've completed a Design Thinking workshop for [project name]. The validated concept is [brief description].
The DT handoff contract is at .copilot-tracking/dt/{slug}/. Please research:

1. Which existing codebase patterns match the solution architecture from our DT output
2. Any external APIs, libraries, or frameworks the solution requires
3. Key integration points and their current state in the codebase
4. Any unknowns or risks that the DT process surfaced that need technical investigation
```

### Output

Task Researcher writes a research document to:

```
.copilot-tracking/research/YYYY-MM-DD-<topic>-research.md
```

This document contains:
- Evidence log with specific file and line references
- Recommended implementation approach with rationale
- Alternatives considered and why they were ruled out
- Open questions or risks

### After research

1. Review the research document carefully
2. Run `/clear` or open a new chat window

---

## Step 3: Plan

```
/task-plan
```

Or select **Task Planner** from the agent picker.

Provide the path to the research document as input:

```
Create an implementation plan based on the research at
.copilot-tracking/research/YYYY-MM-DD-<topic>-research.md.
The DT handoff contract is at .copilot-tracking/dt/{slug}/.
```

### Output

Task Planner writes two files:

```
.copilot-tracking/plans/YYYY-MM-DD-<topic>-plan.md        # Checklist of tasks
.copilot-tracking/plans/YYYY-MM-DD-<topic>-details.md     # Task-by-task details with line references
```

### After planning

1. Review both plan files — all tasks should have specific files and line numbers
2. Run `/clear` or open a new chat window

---

## Step 4: Implement

```
/task-implement
```

Or select **Task Implementor** from the agent picker.

Provide the path to the plan:

```
Implement the plan at .copilot-tracking/plans/YYYY-MM-DD-<topic>-plan.md.
Start with the first unchecked task.
```

### How implementation works

Task Implementor:
- Executes tasks from the plan one by one
- Checks each task off when complete
- Logs all changes to `.copilot-tracking/changes/YYYY-MM-DD-<topic>-changes.md`
- Stops for your review at defined checkpoints

### After implementation

1. Review the changes log and spot-check the code
2. Run any available tests or linters
3. Run `/clear` or open a new chat window

---

## Step 5: Review

```
/task-review
```

Or select **Task Reviewer** from the agent picker.

Provide the research, plan, and changes documents:

```
Review the implementation against:
- Research: .copilot-tracking/research/YYYY-MM-DD-<topic>-research.md
- Plan: .copilot-tracking/plans/YYYY-MM-DD-<topic>-plan.md
- Changes: .copilot-tracking/changes/YYYY-MM-DD-<topic>-changes.md

Validate against the DT acceptance criteria in .copilot-tracking/dt/{slug}/.
```

### Output

Task Reviewer writes:

```
.copilot-tracking/reviews/YYYY-MM-DD-<topic>-review.md
```

This document contains:
- What was implemented vs. planned
- Convention compliance checks
- Gaps or follow-up work identified
- Recommended next iteration (if any)

---

## The Critical Rule: Clear Context Between Phases

> 🔴 **Always use `/clear` or start a new chat between phases.**

Each agent has different instructions. Accumulated context causes errors:

```
DT Coach → /clear → Task Researcher → /clear → Task Planner → /clear → Task Implementor → /clear → Task Reviewer
```

Research findings live in files, not chat history. After clearing, open the relevant `.copilot-tracking/` artifact in your editor before invoking the next agent.

---

## Quick Reference: Prompts & Agents

| Phase | Agent | Prompt Shortcut | Output |
|---|---|---|---|
| DT Handoff | DT Coach | `/dt-handoff-implementation-space` | Handoff contract in `.copilot-tracking/dt/` |
| Research | Task Researcher | `/task-research <topic>` | `research.md` in `.copilot-tracking/research/` |
| Plan | Task Planner | `/task-plan` | `plan.md` + `details.md` in `.copilot-tracking/plans/` |
| Implement | Task Implementor | `/task-implement` | Working code + `changes.md` in `.copilot-tracking/changes/` |
| Review | Task Reviewer | `/task-review` | `review.md` in `.copilot-tracking/reviews/` |

---

## Full Workflow Shortcut

For straightforward tasks, use the **rpi-agent** to orchestrate all phases:

```
/rpi Implement [brief description of solution from DT output].
The DT handoff contract is at .copilot-tracking/dt/{project-slug}/.
```

The rpi-agent coordinates Task Researcher → Task Planner → Task Implementor → Task Reviewer automatically. Use individual agents when you want more control over each phase.

---

## Artifact Directory Structure (Post-RPI)

```
.copilot-tracking/
├── dt/{project-slug}/                 # DT session artifacts (from DT workshop)
│   ├── coaching-state.md
│   ├── method-01-*.md ... method-09-*.md
│   └── [handoff contract]             # Generated by /dt-handoff-implementation-space
├── research/
│   └── YYYY-MM-DD-<topic>-research.md
├── plans/
│   ├── YYYY-MM-DD-<topic>-plan.md
│   └── YYYY-MM-DD-<topic>-details.md
├── changes/
│   └── YYYY-MM-DD-<topic>-changes.md
└── reviews/
    └── YYYY-MM-DD-<topic>-review.md
```

All of these are git-ignored (ephemeral working artifacts).

---

## When to Use Individual Agents vs. rpi-agent

| Scenario | Use |
|---|---|
| Multi-file changes with external dependencies | Individual agents (more control) |
| Unclear requirements or new-to-you codebase | Individual agents (review each phase) |
| Straightforward implementation, familiar codebase | `rpi-agent` (faster) |
| After DT where a full handoff contract exists | Individual agents (ensure DT outputs are respected) |

---

## See Also

- [Greenfield Workshop Guide](./workshop-guide.md) — The 9-method DT framework this follows
- [Brownfield RPI Guide](./brownfield/rpi-guide.md) — RPI for existing system modernization
- [HVE Core RPI Documentation](https://github.com/microsoft/hve-core/blob/main/docs/rpi/README.md) — Upstream reference
