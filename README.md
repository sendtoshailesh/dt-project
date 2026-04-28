# Design Thinking Workshop Toolkit

A reusable toolkit for running **AI-enhanced Design Thinking workshops** using [Microsoft HVE Core](https://github.com/microsoft/hve-core)'s Design Thinking collection with GitHub Copilot.

## What This Is

This repo provides a documented, repeatable setup for running Design Thinking workshops powered by the **DT Coach** agent from HVE Core. It walks you from installation to running a full 9-method Design Thinking process on any problem statement.

## Prerequisites

- [VS Code](https://code.visualstudio.com/) (latest)
- [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension (active subscription)
- [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) extension
- Git & [GitHub CLI (`gh`)](https://cli.github.com/) installed

## Quick Start

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

## Detailed Setup Guide

See [docs/setup-guide.md](docs/setup-guide.md) for the full step-by-step setup instructions.

## Workshop Workflow Guide

See [docs/workshop-guide.md](docs/workshop-guide.md) for how to run each method of the 9-method Design Thinking framework.

## Agents & Prompts Reference

See [docs/reference.md](docs/reference.md) for a complete reference of all DT Coach agents, prompts, and instructions.

## Project Structure

```
dt-project/
├── README.md                  # This file
├── .gitignore                 # Excludes .copilot-tracking/ and other ephemeral files
├── docs/
│   ├── setup-guide.md         # Step-by-step installation & setup
│   ├── workshop-guide.md      # How to run the 9-method DT workshop
│   ├── reference.md           # Agents, prompts, instructions reference
│   └── learnings/             # Accumulated learnings from workshops
│       └── README.md          # Index of learnings
└── .copilot-tracking/         # (git-ignored) Ephemeral DT session artifacts
    └── dt/
        └── {project-slug}/    # Per-project coaching state & artifacts
```

## License

MIT
