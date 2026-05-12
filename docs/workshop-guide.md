# Workshop Guide — The 9-Method Design Thinking Framework

This guide explains each method in the HVE Design Thinking framework and how to use the DT Coach agent to work through them.

---

## Overview

The framework is organized into three **spaces**, each containing three **methods**:

```
┌─────────────────────────────────────────────────────────────────┐
│                    PROBLEM SPACE (Methods 1-3)                  │
│  Discover real problems behind solution requests                │
│                                                                 │
│  Method 1: Scope Conversations                                  │
│  Method 2: Design Research                                      │
│  Method 3: Input Synthesis                                      │
├─────────────────────────────────────────────────────────────────┤
│                   SOLUTION SPACE (Methods 4-6)                  │
│  Develop and validate creative solutions                        │
│                                                                 │
│  Method 4: Brainstorming                                        │
│  Method 5: User Concepts                                        │
│  Method 6: Low-Fidelity Prototypes                              │
├─────────────────────────────────────────────────────────────────┤
│               IMPLEMENTATION SPACE (Methods 7-9)                │
│  Build, test, and scale validated solutions                     │
│                                                                 │
│  Method 7: High-Fidelity Prototypes                             │
│  Method 8: User Testing                                         │
│  Method 9: Iteration at Scale                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Coaching Philosophy: Think → Speak → Empower

Every DT Coach interaction follows this pattern:

1. **Think** — Coach internally considers what questions would surface insights
2. **Speak** — Shares observations conversationally ("I'm noticing...", "This makes me think of...")
3. **Empower** — Ends with choices, not directives ("Does that resonate?", "Want to explore that or move forward?")

The coach works **with** you to discover, not **for** you to deliver.

---

## Problem Space

### Method 1: Scope Conversations

**Goal:** Discover the real problems behind the initial request.

**Key Activities:**
- Determine if the request is "frozen" (fixed solution) or "fluid" (open problem)
- Map stakeholders and their relationships
- Capture the gap between current state and desired state
- Identify assumptions that need validation

**Artifacts Produced:**
- `method-01-stakeholder-map.md` — Stakeholder map with roles and relationships
- `method-01-scope-summary.md` — Scope definition and problem framing

**Prompts:** Use `/dt-method-next` to advance when Method 1 is complete.

---

### Method 2: Design Research

**Goal:** Systematic stakeholder research and observation.

**Key Activities:**
- Plan stakeholder interviews (who, what to ask, what to observe)
- Conduct interviews and record findings
- Identify observation opportunities in existing workflows
- Document research findings systematically

**Artifacts Produced:**
- `method-02-research-plan.md` — Interview and observation plan
- `method-02-interview-notes.md` — Structured interview findings

---

### Method 3: Input Synthesis

**Goal:** Pattern recognition and theme development from research.

**Key Activities:**
- Cluster observations into themes
- Develop "How Might We" (HMW) questions
- Create insight statements that bridge observations to opportunities
- Identify contradictions and tensions in the data

**Artifacts Produced:**
- `method-03-themes.md` — Thematic clusters from research
- `method-03-hmw-questions.md` — How Might We questions for ideation

**Space Handoff:** Use `/dt-handoff-problem-space` to formally summarize Problem Space findings before moving to Solution Space.

---

## Solution Space

### Method 4: Brainstorming

**Goal:** Divergent ideation on validated problems.

**Key Activities:**
- Generate ideas broadly (quantity over quality initially)
- Use HMW questions from Method 3 as brainstorming prompts
- Ideation phase followed by convergence phase
- Vote/prioritize ideas

**Artifacts Produced:**
- `method-04-ideas.md` — Raw brainstorming output
- `method-04-convergence.md` — Prioritized and clustered ideas

**Prompts:** `/dt-method-04-ideation` for ideation, `/dt-method-04-convergence` for convergence voting.

---

### Method 5: User Concepts

**Goal:** Visual concept validation.

**Key Activities:**
- Develop 2–3 concept descriptions from top ideas
- Create concept cards with problem, solution, and value proposition
- Validate concepts against stakeholder needs
- Compare and evaluate concepts

**Artifacts Produced:**
- `method-05-concept-cards.md` — Concept descriptions and cards

**Prompts:** `/dt-method-05-concepts` for concept development, `/dt-method-05-evaluation` for comparison.

---

### Method 6: Low-Fidelity Prototypes

**Goal:** Scrappy constraint discovery through rapid prototyping.

**Key Activities:**
- Build quick, rough prototypes (paper, wireframes, mockups)
- Focus on discovering constraints, not polish
- Test hypotheses about feasibility and desirability
- Gather early feedback

**Artifacts Produced:**
- `method-06-prototype-plan.md` — Prototype scope and hypotheses
- `method-06-test-results.md` — Feedback and constraint findings

**Prompts:** `/dt-method-06-building`, `/dt-method-06-planning`, `/dt-method-06-testing`.

**Space Handoff:** Use `/dt-handoff-solution-space` to formally summarize Solution Space outcomes.

---

## Implementation Space

### Method 7: High-Fidelity Prototypes

**Goal:** Technical feasibility testing with production-quality prototypes.

### Method 8: User Testing

**Goal:** Systematic validation and iteration with real users.

### Method 9: Iteration at Scale

**Goal:** Continuous optimization and preparation for handoff to development.

**Space Handoff:** Use `/dt-handoff-implementation-space` to formally transition to implementation.

---

## Non-Linear Iteration

**Iteration is expected and normal.** You may need to move backward:

- Synthesis (Method 3) reveals gaps → return to Research (Method 2)
- Prototype testing (Method 6) exposes unvalidated assumptions → return to Scope Conversations (Method 1)
- User testing (Method 8) shows concept flaws → return to Concepts (Method 5)

DT Coach tracks these transitions in the coaching state and helps you navigate them.

---

## Session Management

### Starting a Session
```
/dt-start-project project-slug=my-project context="Problem statement" industry=domain
```

### Resuming a Session
```
/dt-resume-coaching project-slug=my-project
```

### Advancing Methods
```
/dt-method-next
```

### Generating Deliverables
```
/dt-canonical-deck       # Generate presentation deck
/dt-figma-export         # Export to FigJam board (requires Figma MCP server)
```

### Handing Off to Development
Use the **"Hand off to RPI"** button in DT Coach, or invoke the task-researcher agent directly. This transitions your validated Design Thinking outputs into the Research → Plan → Implement workflow.

See [docs/rpi-guide.md](./rpi-guide.md) for a step-by-step guide to the post-DT RPI workflow.

---

## Progressive Hint Engine

When you're stuck, DT Coach uses a 4-level escalation:

| Level | Style | Example |
|---|---|---|
| 1 | Broad direction | "What else did they mention?" |
| 2 | Contextual focus | "You're on the right track with X. What about Y?" |
| 3 | Specific area | "They mentioned [topic]. What challenges might that create?" |
| 4 | Direct detail | Specific quotes or details (last resort) |
