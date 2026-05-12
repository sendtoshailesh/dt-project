# Design Thinking Workshop Toolkit

A reusable toolkit for running **AI-enhanced Design Thinking workshops** using [Microsoft HVE Core](https://github.com/microsoft/hve-core)'s Design Thinking collection with GitHub Copilot.

Supports both **greenfield projects** (starting from scratch) and **brownfield projects** (improving or modernizing existing systems).

## What This Is

This repo provides a documented, repeatable setup for running Design Thinking workshops powered by the **DT Coach** agent from HVE Core. It walks you from installation to running a full 9-method Design Thinking process on any problem statement.

Two scaffolds are provided:

| Scaffold | When to Use |
|---|---|
| **Greenfield** (default) | Starting from scratch — no existing system or codebase |
| **Brownfield** | Existing system in production — improving, modernizing, or migrating |

## Prerequisites

- [VS Code](https://code.visualstudio.com/) (latest)
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension (active subscription)
- [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) extension
- Git & [GitHub CLI (`gh`)](https://cli.github.com/) installed

## Quick Start

### Greenfield Project (starting from scratch)

```bash
# 1. Clone this repo
git clone https://github.com/sendtoshailesh/dt-project.git
cd dt-project

# 2. Install the HVE Design Thinking extension
code --install-extension ise-hve-essentials.hve-design-thinking

# 3. Open in VS Code
code .

# 4. Launch Copilot Chat (Ctrl+Alt+I) and start a project
#    Select DT Coach from the @ agent picker, then run:
/dt-start-project project-slug=my-project context="Your problem statement here" industry=your-industry
```

### Brownfield Project (existing system)

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

# 5. Complete System Discovery (Phase 0) — see docs/brownfield/setup-guide.md
#    Create: system-inventory.md, technical-debt-map.md, integration-constraints.md

# 6. Launch Copilot Chat and start with brownfield parameters:
/dt-start-project project-slug=my-brownfield-project context="What needs to change" industry=your-industry project-type=brownfield existing-system="Brief description of the existing system"
```

## Detailed Setup Guide

- **Greenfield:** See [docs/setup-guide.md](docs/setup-guide.md) for the full step-by-step setup instructions.
- **Brownfield:** See [docs/brownfield/setup-guide.md](docs/brownfield/setup-guide.md) for setup including System Discovery Phase.

## Workshop Workflow Guide

- **Greenfield:** See [docs/workshop-guide.md](docs/workshop-guide.md) for how to run each method of the 9-method Design Thinking framework.
- **Brownfield:** See [docs/brownfield/workshop-guide.md](docs/brownfield/workshop-guide.md) for the brownfield-adapted 9-method guide.

## Agents & Prompts Reference

- **Greenfield:** See [docs/reference.md](docs/reference.md) for a complete reference of all DT Coach agents, prompts, and instructions.
- **Brownfield:** See [docs/brownfield/reference.md](docs/brownfield/reference.md) for brownfield-specific agents, prompts, and artifact templates.

## Project Structure

```
dt-project/
├── README.md                  # This file
├── .gitignore                 # Excludes .copilot-tracking/ and other ephemeral files
├── docs/
│   ├── setup-guide.md         # Greenfield: step-by-step installation & setup
│   ├── workshop-guide.md      # Greenfield: how to run the 9-method DT workshop
│   ├── reference.md           # Greenfield: agents, prompts, instructions reference
│   ├── brownfield/
│   │   ├── README.md          # Brownfield scaffold overview
│   │   ├── setup-guide.md     # Brownfield: setup including System Discovery Phase
│   │   ├── workshop-guide.md  # Brownfield: 9-method guide adapted for existing systems
│   │   └── reference.md       # Brownfield: agents, prompts, and artifact templates
│   └── learnings/             # Accumulated learnings from workshops (greenfield + brownfield)
│       └── README.md          # Index of learnings
└── .copilot-tracking/         # (git-ignored) Ephemeral DT session artifacts
    └── dt/
        └── {project-slug}/    # Per-project coaching state & artifacts
            ├── coaching-state.md
            ├── system-inventory.md          # (brownfield only)
            ├── technical-debt-map.md        # (brownfield only)
            ├── integration-constraints.md   # (brownfield only)
            └── method-01-*.md ... method-09-*.md
```

## License

MIT
