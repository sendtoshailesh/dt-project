# Setup Guide — Design Thinking Workshop Toolkit

This guide documents every step to set up the HVE Core Design Thinking environment from scratch.

---

## Step 1: Install VS Code Extensions

### Required Extensions

| Extension | Install Command |
|---|---|
| GitHub Copilot | `code --install-extension GitHub.copilot` |
| GitHub Copilot Chat | `code --install-extension GitHub.copilot-chat` |
| HVE Design Thinking | `code --install-extension ise-hve-essentials.hve-design-thinking` |

> **Alternative:** Install the full HVE suite with `code --install-extension ise-hve-essentials.hve-core-all` to get all 221 artifacts across all domains (not just Design Thinking).

### Verify Installation

```bash
code --list-extensions | grep -i hve
# Expected: ise-hve-essentials.hve-design-thinking
```

## Step 2: Initialize Your Project

```bash
# Create project directory
mkdir dt-project && cd dt-project

# Initialize git
git init

# Create .gitignore (exclude ephemeral DT artifacts)
echo ".copilot-tracking/" > .gitignore
```

## Step 3: Create the DT Tracking Directory

HVE Design Thinking stores all coaching artifacts under `.copilot-tracking/dt/{project-slug}/`. Create this for each new workshop:

```bash
# Replace "my-project" with a kebab-case identifier for your problem
mkdir -p .copilot-tracking/dt/my-project
```

## Step 4: Verify DT Coach Agent Is Available

1. Open the project in VS Code: `code .`
2. Open Copilot Chat: `Ctrl+Alt+I` (Windows/Linux) or `Cmd+Alt+I` (Mac)
3. Type `@` in the chat input
4. Confirm **DT Coach** appears in the agent picker list

> **Troubleshooting:** If DT Coach doesn't appear, reload VS Code (`Ctrl+Shift+P` → "Developer: Reload Window"). The extension needs a reload after first install.

## Step 5: Start a Design Thinking Project

In Copilot Chat, invoke the start prompt:

```
/dt-start-project project-slug=my-project context="Your problem statement" industry=your-industry
```

### Parameters

| Parameter | Required | Description | Example |
|---|---|---|---|
| `project-slug` | Yes | Kebab-case project identifier | `sponsor-discount-reconciliation` |
| `context` | Optional | Problem statement or customer request | `"The platform cannot apply discounts..."` |
| `stakeholders` | Optional | Known stakeholder groups | `"sponsors, merchants, finance team"` |
| `industry` | Optional | Domain context for coaching vocabulary | `fintech`, `healthcare`, `manufacturing` |

### What Happens Next

DT Coach walks you through **Phase 1: Session Initialization**:
1. Clarifies your role, team, and context
2. Asks which Design Thinking method to start with (default: Method 1)
3. Asks whether to enable the **canonical deck workflow** (opt-in for PowerPoint deck generation)
4. Confirms session objectives

Then transitions to **Phase 2: Active Coaching** for your chosen method.

## Step 6: Resume a Previous Session

```
/dt-resume-coaching project-slug=my-project
```

DT Coach reads the coaching state file and picks up where you left off.

---

## Extension Options Comparison

| Extension | ID | What You Get |
|---|---|---|
| **HVE Design Thinking** | `hve-design-thinking` | 2 agents, 13 prompts, 43 instructions — DT only |
| **HVE Core All** | `hve-core-all` | 51 agents, 63 prompts, 102 instructions, 12 skills — everything |
| **HVE Installer** | `hve-installer` | Selective collection installer — pick what you need |

For Design Thinking workshops only, `hve-design-thinking` is sufficient. For a full engineering workflow (DT → RPI → implementation), use `hve-core-all`.

## Repeating for a New Workshop

To start a fresh workshop on a different problem:

```bash
# 1. Create a new tracking directory
mkdir -p .copilot-tracking/dt/new-problem-slug

# 2. In Copilot Chat, start a new project
/dt-start-project project-slug=new-problem-slug context="New problem statement" industry=your-industry
```

Each project gets its own coaching state and artifacts under `.copilot-tracking/dt/{slug}/`.
