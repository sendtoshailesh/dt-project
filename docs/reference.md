# Reference — Agents, Prompts & Instructions

Complete reference for all Design Thinking components from [microsoft/hve-core](https://github.com/microsoft/hve-core).

---

## Agents (2)

| Agent | Description |
|---|---|
| **DT Coach** | Primary coaching agent — guides teams through the 9-method HVE Design Thinking framework using Think/Speak/Empower philosophy |
| **DT Coach** (via handoffs) | Same agent, re-invoked for method transitions and canonical deck operations |

### DT Coach Handoff Buttons

When using DT Coach in VS Code, these quick-action buttons appear:

| Button | Target | Description |
|---|---|---|
| 🎯 Method Next | DT Coach | Advance to next DT method |
| 📋 Canonical Deck | DT Coach | Generate presentation deck |
| 🖼️ Build Customer Cards PPTX | DT Coach | Generate PowerPoint customer cards |
| 🔬 Hand off to RPI | Task Researcher | Transition to RPI development workflow |
| 📋 Export to Figma | DT Coach | Export artifacts to FigJam board |

---

## Prompts (13)

### Project Lifecycle

| Prompt | Description |
|---|---|
| `/dt-start-project` | Initialize a new DT coaching project with state and first interaction |
| `/dt-resume-coaching` | Resume a previous session — reads coaching state, re-establishes context |
| `/dt-method-next` | Advance to the next method in sequence |

### Method-Specific

| Prompt | Method | Description |
|---|---|---|
| `/dt-method-04-ideation` | 4 | Divergent ideation phase of brainstorming |
| `/dt-method-04-convergence` | 4 | Convergence and voting phase |
| `/dt-method-05-concepts` | 5 | Concept development |
| `/dt-method-05-evaluation` | 5 | Concept comparison and evaluation |
| `/dt-method-06-building` | 6 | Prototype building |
| `/dt-method-06-planning` | 6 | Prototype planning |
| `/dt-method-06-testing` | 6 | Prototype testing |

### Handoffs & Deliverables

| Prompt | Description |
|---|---|
| `/dt-handoff-problem-space` | Summarize Problem Space (Methods 1-3) findings |
| `/dt-handoff-solution-space` | Summarize Solution Space (Methods 4-6) outcomes |
| `/dt-handoff-implementation-space` | Transition to implementation |
| `/dt-canonical-deck` | Generate canonical presentation deck from artifacts |
| `/dt-figma-export` | Export artifacts to FigJam board |

---

## Instructions (43) — Auto-Loaded

Instructions load automatically based on which files are open. You don't invoke these directly.

### Ambient (always active when DT project is open)

| Instruction | Purpose |
|---|---|
| `dt-coaching-identity` | Think/Speak/Empower philosophy, progressive hint engine, hat-switching |
| `dt-coaching-state` | YAML state schema, session recovery, state management rules |
| `dt-method-sequencing` | Method transition rules, 9-method sequence, space boundaries |
| `dt-quality-constraints` | Fidelity rules and output quality standards |
| `dt-canonical-deck` | Canonical deck and customer-card generation workflow |

### Per-Method (loaded when working in that method)

| Instruction | Method |
|---|---|
| `dt-method-01-scope` | Method 1: Scope Conversations |
| `dt-method-01-deep` | Method 1: Deep expertise |
| `dt-method-02-research` | Method 2: Design Research |
| `dt-method-02-deep` | Method 2: Deep expertise |
| `dt-method-03-synthesis` | Method 3: Input Synthesis |
| `dt-method-03-deep` | Method 3: Deep expertise |
| `dt-method-04-brainstorming` | Method 4: Brainstorming |
| `dt-method-04-deep` | Method 4: Deep expertise |
| `dt-method-05-concepts` | Method 5: User Concepts |
| `dt-method-05-deep` | Method 5: Deep expertise |
| `dt-method-06-lofi-prototypes` | Method 6: Low-Fi Prototypes |
| `dt-method-06-deep` | Method 6: Deep expertise |
| `dt-method-07-hifi-prototypes` | Method 7: High-Fi Prototypes |
| `dt-method-07-deep` | Method 7: Deep expertise |
| `dt-method-08-testing` | Method 8: User Testing |
| `dt-method-08-deep` | Method 8: Deep expertise |
| `dt-method-09-iteration` | Method 9: Iteration at Scale |
| `dt-method-09-deep` | Method 9: Deep expertise |

### Curriculum (educational scaffolding)

| Instruction | Method |
|---|---|
| `dt-curriculum-01-scoping` | Scoping curriculum |
| `dt-curriculum-02-research` | Research curriculum |
| `dt-curriculum-03-synthesis` | Synthesis curriculum |
| `dt-curriculum-04-brainstorming` | Brainstorming curriculum |
| `dt-curriculum-05-concepts` | Concepts curriculum |
| `dt-curriculum-06-prototypes` | Prototypes curriculum |
| `dt-curriculum-07-testing` | Testing curriculum |
| `dt-curriculum-08-iteration` | Iteration curriculum |
| `dt-curriculum-09-handoff` | Handoff curriculum |
| `dt-curriculum-scenario-manufacturing` | Manufacturing scenario |

### Industry-Specific

| Instruction | Industry |
|---|---|
| `dt-industry-healthcare` | Healthcare domain vocabulary and constraints |
| `dt-industry-manufacturing` | Manufacturing domain vocabulary and constraints |
| `dt-industry-energy` | Energy domain vocabulary and constraints |

### Other

| Instruction | Purpose |
|---|---|
| `dt-image-prompt-generation` | Generate image prompts for DT artifacts |
| `dt-rpi-handoff-contract` | Contract for DT → RPI handoff |
| `dt-rpi-implement-context` | Implementation context for RPI |
| `dt-rpi-plan-context` | Planning context for RPI |

---

## Artifact Storage

All artifacts are stored under:
```
.copilot-tracking/dt/{project-slug}/
├── coaching-state.md        # YAML coaching state (method, progress, session log)
├── method-01-*.md           # Method 1 artifacts
├── method-02-*.md           # Method 2 artifacts
├── ...
└── method-09-*.md           # Method 9 artifacts
```

This directory is git-ignored. Artifacts are ephemeral coaching outputs, not version-controlled deliverables.
