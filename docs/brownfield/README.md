# Brownfield SDLC Scaffold — Design Thinking Toolkit

This scaffold adapts the HVE Design Thinking framework for **brownfield projects** — situations where you are working with an **existing system, codebase, or product** rather than starting from scratch.

---

## Greenfield vs. Brownfield

| Dimension | Greenfield | Brownfield |
|---|---|---|
| Starting point | Blank slate | Existing system in production |
| Primary constraint | Possibility space | Legacy, integration, migration |
| Research includes | Future-state user needs | Current-system pain points + user needs |
| Prototyping includes | Unconstrained concepts | Integration-aware POCs |
| Implementation includes | Build from scratch | Migrate, extend, or replace |
| Key risk | Over-engineering | Disrupting working system |

---

## When to Use the Brownfield Scaffold

Use this scaffold when **any** of these conditions apply:

- There is an existing system, application, or product that real users depend on
- The problem statement includes words like: "improve", "modernize", "replace", "migrate", "extend", "refactor", or "fix"
- The engineering team inherits code they did not write
- There are integration points (APIs, data stores, downstream consumers) that must remain working
- Users have existing workflows that cannot be broken without change management

> **If you have zero existing code or system:** use the standard [greenfield scaffold](../setup-guide.md) instead.

---

## How the Brownfield Scaffold Differs

The brownfield scaffold adds a **System Discovery Phase** before Design Thinking begins, and adds brownfield-specific guidance to each of the 9 DT methods:

```
┌─────────────────────────────────────────────────────────────────┐
│               PHASE 0: SYSTEM DISCOVERY (Brownfield only)       │
│  Understand the existing system before designing its future     │
│                                                                 │
│  0a. System Inventory (components, users, integrations)         │
│  0b. Technical Debt & Pain Point Mapping                        │
│  0c. Integration & Dependency Constraints                       │
├─────────────────────────────────────────────────────────────────┤
│                    PROBLEM SPACE (Methods 1-3)                  │
│  Discover real problems — anchored in the existing system       │
│                                                                 │
│  Method 1: Scope Conversations (+ legacy constraint framing)    │
│  Method 2: Design Research (+ system archaeology)               │
│  Method 3: Input Synthesis (+ debt vs. need tension mapping)    │
├─────────────────────────────────────────────────────────────────┤
│                   SOLUTION SPACE (Methods 4-6)                  │
│  Develop solutions that fit within or replace existing system   │
│                                                                 │
│  Method 4: Brainstorming (+ migrate/extend/replace framing)     │
│  Method 5: User Concepts (+ migration strategy options)         │
│  Method 6: Low-Fidelity Prototypes (+ integration constraints)  │
├─────────────────────────────────────────────────────────────────┤
│               IMPLEMENTATION SPACE (Methods 7-9)                │
│  Build, test, and scale — with migration path clarity           │
│                                                                 │
│  Method 7: High-Fidelity Prototypes (+ real system integration) │
│  Method 8: User Testing (+ change management for existing users)│
│  Method 9: Iteration at Scale (+ technical migration path)      │
└─────────────────────────────────────────────────────────────────┘
```

---

## Quick Start

```bash
# 1. Clone this repo
git clone https://github.com/sendtoshailesh/dt-project.git
cd dt-project

# 2. Install the HVE Design Thinking extension
code --install-extension ise-hve-essentials.hve-design-thinking

# 3. Open in VS Code
code .

# 4. Create a brownfield project tracking directory
mkdir -p .copilot-tracking/dt/my-brownfield-project

# 5. Launch Copilot Chat (Ctrl+Alt+I) and start with system discovery:
/dt-start-project project-slug=my-brownfield-project \
  context="Your problem statement here" \
  industry=your-industry \
  project-type=brownfield \
  existing-system="Brief description of the existing system"
```

---

## Guides

| Guide | Description |
|---|---|
| [Setup Guide](./setup-guide.md) | Step-by-step setup including System Discovery Phase |
| [Workshop Guide](./workshop-guide.md) | Brownfield-adapted 9-method DT framework |
| [Reference](./reference.md) | Brownfield-specific agents, prompts, and artifact templates |
| [RPI Guide](./rpi-guide.md) | Post-DT migration-focused Research, Plan, Implement, Review workflow |

---

## Project Structure (Brownfield)

```
dt-project/
├── README.md
├── .gitignore
├── docs/
│   ├── setup-guide.md              # Greenfield setup
│   ├── workshop-guide.md           # Greenfield workshop guide
│   ├── reference.md                # Greenfield reference
│   ├── rpi-guide.md                # Greenfield post-DT RPI workflow
│   ├── brownfield/
│   │   ├── README.md               # This file
│   │   ├── setup-guide.md          # Brownfield setup (System Discovery + DT)
│   │   ├── workshop-guide.md       # Brownfield-adapted 9-method DT guide
│   │   ├── reference.md            # Brownfield agents, prompts, and artifacts
│   │   └── rpi-guide.md            # Brownfield post-DT migration RPI workflow
│   └── learnings/
│       └── README.md               # Learnings index (greenfield + brownfield)
└── .copilot-tracking/              # (git-ignored) ephemeral session artifacts
    └── dt/
        └── {project-slug}/
            ├── coaching-state.md
            ├── system-inventory.md          # Brownfield: existing system catalog
            ├── technical-debt-map.md        # Brownfield: pain points + debt
            ├── integration-constraints.md   # Brownfield: integration map
            ├── migration-strategy.md        # Brownfield: transition approach
            └── method-01-*.md ... method-09-*.md
```
