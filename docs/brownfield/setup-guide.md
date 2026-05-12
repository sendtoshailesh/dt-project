# Setup Guide — Brownfield SDLC Design Thinking Scaffold

This guide covers every step to set up and run a Design Thinking workshop for a **brownfield project** — one where an existing system, product, or codebase already exists in production.

The key difference from the [greenfield setup guide](../setup-guide.md) is **Phase 0: System Discovery**, which you complete before invoking the DT Coach agent.

---

## Step 1: Install VS Code Extensions

Same as the greenfield setup — no changes needed.

| Extension | Install Command |
|---|---|
| GitHub Copilot | `code --install-extension GitHub.copilot` |
| GitHub Copilot Chat | `code --install-extension GitHub.copilot-chat` |
| HVE Design Thinking | `code --install-extension ise-hve-essentials.hve-design-thinking` |

> **Full engineering workflow** (DT → RPI → implementation): use `code --install-extension ise-hve-essentials.hve-core-all` to get all agents across Design Thinking, Research, Planning, and Implementation domains.

### Verify Installation

```bash
code --list-extensions | grep -i hve
# Expected: ise-hve-essentials.hve-design-thinking
```

---

## Step 2: Initialize Your Project Directory

```bash
# Create or navigate to the project directory
mkdir dt-project && cd dt-project

# Initialize git (if not already a git repo)
git init

# Ensure .gitignore excludes ephemeral DT artifacts
echo ".copilot-tracking/" >> .gitignore

# Create a brownfield project tracking directory
mkdir -p .copilot-tracking/dt/my-brownfield-project
```

---

## Step 3: Phase 0 — System Discovery (Brownfield-Specific)

Before invoking the DT Coach, capture the existing system's context. This gives the coach the grounding it needs to provide brownfield-relevant coaching throughout all 9 methods.

Create the following files in `.copilot-tracking/dt/{project-slug}/`:

### 3a. System Inventory (`system-inventory.md`)

Document the existing system components:

```bash
cat > .copilot-tracking/dt/my-brownfield-project/system-inventory.md << 'EOF'
# System Inventory

**Project:** my-brownfield-project
**Date:** YYYY-MM-DD
**Author:** [Your name]

## System Overview

[1–3 paragraph description of the existing system: what it does, who uses it, how long it has been in production]

## Components

| Component | Technology | Owner | Status |
|---|---|---|---|
| [e.g. Web Frontend] | [e.g. React 16, jQuery] | [Team] | [Active / Deprecated] |
| [e.g. REST API] | [e.g. Java Spring Boot] | [Team] | [Active] |
| [e.g. Database] | [e.g. PostgreSQL 12] | [Team] | [Active] |

## User Groups

| User Group | Count (approx.) | How They Interact |
|---|---|---|
| [e.g. End customers] | [e.g. ~50,000 monthly] | [e.g. Web + mobile app] |
| [e.g. Operations team] | [e.g. ~20 internal] | [e.g. Admin dashboard] |

## Key Integrations & Dependencies

| System | Direction | Protocol | Criticality |
|---|---|---|---|
| [e.g. Payment gateway] | Outbound | REST | Critical |
| [e.g. ERP system] | Inbound | SFTP batch | High |

## Data Assets

[Describe key data entities, estimated volume, any regulatory or compliance considerations]
EOF
```

### 3b. Technical Debt Map (`technical-debt-map.md`)

Capture known pain points, bugs, and debt before DT begins:

```bash
cat > .copilot-tracking/dt/my-brownfield-project/technical-debt-map.md << 'EOF'
# Technical Debt Map

**Project:** my-brownfield-project
**Date:** YYYY-MM-DD

## Known Pain Points

### User-Facing Pain Points
- [e.g. Checkout flow times out after 30 s under load]
- [e.g. Mobile experience is not responsive — built for desktop]
- [e.g. Error messages are cryptic and unhelpful]

### Operational Pain Points
- [e.g. Deployments require 4-hour maintenance window]
- [e.g. No automated monitoring — alerts come from users]
- [e.g. On-call team spends 6 h/week on manual reconciliation jobs]

### Technical Debt
- [e.g. Authentication uses deprecated OAuth 1.0 library]
- [e.g. 40% test coverage, concentrated in non-critical paths]
- [e.g. Monolithic service — a single deploy touches all domains]
- [e.g. Database schema has no migrations framework]

## Impact Assessment

| Pain Point | Severity (H/M/L) | Frequency | Affected Users |
|---|---|---|---|
| [Checkout timeout] | H | Daily | All customers |
| [Manual reconciliation] | M | Weekly | Finance team |

## Constraints

[Document anything that CANNOT change: regulatory requirements, contractual SLAs, third-party contracts, data residency rules]
EOF
```

### 3c. Integration Constraints (`integration-constraints.md`)

Capture what the future solution must remain compatible with:

```bash
cat > .copilot-tracking/dt/my-brownfield-project/integration-constraints.md << 'EOF'
# Integration Constraints

**Project:** my-brownfield-project
**Date:** YYYY-MM-DD

## Non-Negotiable Interfaces

[List APIs, data formats, or protocols that any new solution MUST support without breaking existing consumers]

| Interface | Consumer | Format | Why Non-Negotiable |
|---|---|---|---|
| [e.g. GET /api/v1/orders] | [Mobile app v2] | [JSON] | [Cannot force all users to upgrade immediately] |
| [e.g. Order export CSV] | [Finance ERP import] | [CSV, fixed columns] | [ERP contract ends in 18 months] |

## Negotiable Interfaces (With Notice Period)

[Interfaces that CAN change but require a migration plan and deprecation window]

| Interface | Current Consumer(s) | Migration Window |
|---|---|---|
| [e.g. Legacy SOAP endpoint] | [Internal reporting tool] | [6 months] |

## Data Migration Constraints

- [e.g. Historical orders must be preserved — 5 years retention required by regulation]
- [e.g. Customer PII must remain in EU region]
- [e.g. Zero data loss is required — no acceptable downtime window for migration]

## Infrastructure Constraints

- [e.g. Must run on-premises — cloud migration is out of scope]
- [e.g. Current CI/CD is Jenkins — replacing pipeline is out of scope]
EOF
```

---

## Step 4: Verify DT Coach Agent Is Available

1. Open the project in VS Code: `code .`
2. Open Copilot Chat: `Ctrl+Alt+I` (Windows/Linux) or `Cmd+Alt+I` (Mac)
3. Type `@` in the chat input
4. Confirm **DT Coach** appears in the agent picker list

> **Troubleshooting:** If DT Coach doesn't appear, reload VS Code (`Ctrl+Shift+P` → "Developer: Reload Window").

---

## Step 5: Start a Brownfield Design Thinking Project

In Copilot Chat, invoke the start prompt with brownfield parameters:

```
/dt-start-project project-slug=my-brownfield-project context="Your problem statement" industry=your-industry project-type=brownfield existing-system="Brief description of existing system and its key pain points"
```

### Parameters

| Parameter | Required | Description | Brownfield Example |
|---|---|---|---|
| `project-slug` | Yes | Kebab-case project identifier | `order-platform-modernization` |
| `context` | Optional | Problem statement | `"The checkout service times out under load and cannot support mobile users"` |
| `stakeholders` | Optional | Known stakeholder groups | `"customers, ops team, finance team, mobile engineers"` |
| `industry` | Optional | Domain context | `fintech`, `healthcare`, `manufacturing` |
| `project-type` | Optional | `brownfield` signals to DT Coach to apply brownfield coaching mode | `brownfield` |
| `existing-system` | Optional | Short description of the existing system | `"Java monolith, 5 years old, PostgreSQL, 50k daily users"` |

### What Happens Next

DT Coach walks you through **Phase 1: Session Initialization** with brownfield awareness:

1. Acknowledges the existing system context from your System Discovery artifacts
2. Clarifies scope: What must change? What must stay the same?
3. Identifies which stakeholders own the existing system versus the future state
4. Asks whether to enable the canonical deck workflow (opt-in for PowerPoint output)
5. Confirms session objectives

Then transitions to **Phase 2: Active Coaching** starting with Method 1 (Scope Conversations) anchored in the brownfield context.

---

## Step 6: Resume a Previous Session

```
/dt-resume-coaching project-slug=my-brownfield-project
```

DT Coach reads the coaching state file (which includes brownfield context) and picks up where you left off.

---

## Extension Options

| Extension | ID | What You Get |
|---|---|---|
| **HVE Design Thinking** | `hve-design-thinking` | 2 agents, 13 prompts, 43 instructions — DT only |
| **HVE Core All** | `hve-core-all` | 51 agents, 63 prompts, 102 instructions, 12 skills — full workflow |
| **HVE Installer** | `hve-installer` | Selective collection installer |

For brownfield modernization projects that will proceed to implementation, **HVE Core All** is recommended: it includes not just Design Thinking but also Research, Planning, and Implementation agents that handle technical migration work.

---

## Starting a New Brownfield Workshop on a Different System

```bash
# 1. Create a new tracking directory
mkdir -p .copilot-tracking/dt/new-system-slug

# 2. Create System Discovery artifacts (repeat Step 3 for the new system)
# system-inventory.md, technical-debt-map.md, integration-constraints.md

# 3. In Copilot Chat, start a new brownfield project
/dt-start-project project-slug=new-system-slug context="New problem statement" industry=domain project-type=brownfield
```
