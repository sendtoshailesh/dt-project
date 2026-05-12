# Workshop Guide — Brownfield Design Thinking Framework

This guide adapts the 9-method HVE Design Thinking framework for **brownfield projects**. Each method retains its core objective but adds brownfield-specific activities, prompts, and artifacts.

Before starting, complete [Phase 0: System Discovery](./setup-guide.md#step-3-phase-0--system-discovery-brownfield-specific) from the setup guide.

---

## Framework Overview

```
┌─────────────────────────────────────────────────────────────────┐
│               PHASE 0: SYSTEM DISCOVERY (Brownfield only)       │
│                                                                 │
│  0a. System Inventory        → system-inventory.md             │
│  0b. Technical Debt Map      → technical-debt-map.md           │
│  0c. Integration Constraints → integration-constraints.md      │
├─────────────────────────────────────────────────────────────────┤
│                    PROBLEM SPACE (Methods 1-3)                  │
│                                                                 │
│  Method 1: Scope Conversations                                  │
│  Method 2: Design Research                                      │
│  Method 3: Input Synthesis                                      │
├─────────────────────────────────────────────────────────────────┤
│                   SOLUTION SPACE (Methods 4-6)                  │
│                                                                 │
│  Method 4: Brainstorming                                        │
│  Method 5: User Concepts                                        │
│  Method 6: Low-Fidelity Prototypes                              │
├─────────────────────────────────────────────────────────────────┤
│               IMPLEMENTATION SPACE (Methods 7-9)                │
│                                                                 │
│  Method 7: High-Fidelity Prototypes                             │
│  Method 8: User Testing                                         │
│  Method 9: Iteration at Scale                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Coaching Philosophy: Think → Speak → Empower

The same philosophy applies in brownfield contexts — the DT Coach always:

1. **Think** — Internally considers questions that surface insights about both user needs and system constraints
2. **Speak** — Shares observations conversationally, including observations about existing-system dynamics
3. **Empower** — Ends with choices: "Do we need to understand the current system better, or do we have enough to move forward?"

In brownfield work, a recurring coaching tension is: _"Is this a problem with the system, or a problem with how users work around the system?"_ The coach surfaces this tension intentionally.

---

## Phase 0: System Discovery

> Complete before starting DT. Outputs feed directly into Method 1.

### 0a. System Inventory

**Goal:** Establish shared understanding of what exists before designing what should exist.

**Key Questions:**
- What does the system currently do well (keep)?
- What does it do poorly (fix or replace)?
- Who depends on it, and how deeply?
- What is the system's rough age, technology stack, and maintenance status?

**Artifact:** `system-inventory.md` (see [setup guide template](./setup-guide.md#3a-system-inventory-system-inventorymd))

---

### 0b. Technical Debt Map

**Goal:** Name and rank the pain points so that DT methods 1–3 can investigate root causes rather than symptoms.

**Key Questions:**
- What are the top 5 user-facing pain points?
- What are the top 5 operational pain points?
- What technical debt is silently limiting all teams?
- Which constraints are truly non-negotiable vs. assumed constraints?

**Artifact:** `technical-debt-map.md` (see [setup guide template](./setup-guide.md#3b-technical-debt-map-technical-debt-mapmd))

---

### 0c. Integration Constraints

**Goal:** Understand the "system envelope" — what any future solution must stay compatible with.

**Key Questions:**
- Which interfaces have external consumers that cannot be changed on your schedule?
- What data must never be lost, corrupted, or migrated unsafely?
- What regulatory or contractual obligations constrain the solution space?

**Artifact:** `integration-constraints.md` (see [setup guide template](./setup-guide.md#3c-integration-constraints-integration-constraintsmd))

---

## Problem Space

### Method 1: Scope Conversations

**Goal:** Discover the real problems behind the initial request — anchored in the existing system reality.

**Brownfield Additions:**

- **Frozen vs. Fluid (revisited):** In brownfield work, requests are often "frozen" because stakeholders come with a predefined solution ("we need to rewrite the checkout service"). The coach helps distinguish: is the *problem* frozen, or just the proposed *solution*?
- **Current-State Baseline:** What does success look like in the current system? What KPIs, SLAs, or user satisfaction scores exist today? Improvement must be measured against a baseline.
- **Stakeholder Ownership Map:** Who owns the existing system (maintenance, ops, on-call)? Their voices are often missing from initial scope conversations but are critical brownfield stakeholders.
- **Constraint Inheritance:** Which constraints from Phase 0 are truly fixed vs. assumed? Scope conversations often reveal that "we can't change X" is an assumption, not a fact.

**Key Activities:**
- Review the System Inventory and Technical Debt Map as input
- Determine if the request is about fixing symptoms vs. root causes
- Map stakeholders — including existing system owners and on-call responders
- Capture the gap between current state metrics and desired state
- Identify which Phase 0 constraints are real vs. inherited assumptions

**Brownfield-Specific Artifacts:**
- `method-01-stakeholder-map.md` — Includes existing system owners and operations team
- `method-01-scope-summary.md` — Documents current-state baseline alongside desired-state vision
- `method-01-constraint-validation.md` *(brownfield addition)* — Which Phase 0 constraints survived stakeholder scrutiny?

**Prompts:**
```
/dt-method-next
```

---

### Method 2: Design Research

**Goal:** Systematic stakeholder research and observation — including the system itself as a source of evidence.

**Brownfield Additions:**

- **System Archaeology:** Treat the existing codebase and its operational data as a research artifact. Support tickets, error logs, performance dashboards, and deployment histories are qualitative and quantitative research data.
- **Shadow Operations:** Observe how users actually work with (and around) the existing system — not just how they're supposed to use it. Brownfield systems accumulate workarounds that reveal real pain.
- **Before/After Journey Mapping:** Document the current user journey through the existing system (with its pain points) as a baseline to design against.
- **Ops & Support Research:** Interview operations and support teams — they have signal on systemic failures that product teams often lack.

**Key Activities:**
- Plan stakeholder interviews — include system owners, ops, and support teams
- Analyze existing telemetry: error rates, latency, support ticket themes
- Observe users' workarounds (spreadsheets, copy-paste, manual steps around the system)
- Map the current user journey through the existing system end-to-end
- Document research findings systematically

**Brownfield-Specific Artifacts:**
- `method-02-research-plan.md` — Includes system archaeology and ops interview plan
- `method-02-interview-notes.md` — Structured findings from interviews
- `method-02-current-journey-map.md` *(brownfield addition)* — As-is user journey through existing system with pain annotations

---

### Method 3: Input Synthesis

**Goal:** Pattern recognition and theme development — surfacing the tensions unique to brownfield change.

**Brownfield Additions:**

- **Debt vs. Need Tension:** The most common brownfield synthesis tension: which problems are caused by technical debt vs. genuine unmet user needs? Both are valid but require different solutions. The coach helps separate them.
- **Keep / Fix / Replace Framework:** Cluster insights into three categories:
  - **Keep:** What works well and must be preserved
  - **Fix:** What exists but is broken and can be repaired incrementally
  - **Replace:** What is so fundamentally wrong it needs to be rebuilt
- **Assumption Surfacing:** Brownfield projects accumulate organizational assumptions about what's possible. Synthesis is a good moment to challenge them.
- **How Might We (Brownfield edition):** HMW questions should address both user needs and system constraints: "How might we reduce checkout timeout without replacing the entire payment service?"

**Key Activities:**
- Cluster observations into themes using Keep/Fix/Replace as a secondary lens
- Develop HMW questions that are constraint-aware (not constraint-ignorant)
- Identify debt-driven vs. need-driven pain points
- Surface inherited organizational assumptions for explicit challenge

**Brownfield-Specific Artifacts:**
- `method-03-themes.md` — Thematic clusters including Keep/Fix/Replace categorization
- `method-03-hmw-questions.md` — HMW questions with brownfield constraint awareness
- `method-03-keep-fix-replace.md` *(brownfield addition)* — Explicit inventory of what to preserve, improve, and retire

**Space Handoff:**
```
/dt-handoff-problem-space
```

---

## Solution Space

### Method 4: Brainstorming

**Goal:** Divergent ideation — explicitly structured around brownfield solution patterns.

**Brownfield Additions:**

- **Brownfield Solution Patterns:** Start brainstorming with established brownfield patterns as framing lenses (not constraints):
  - **Strangler Fig:** Gradually replace parts of the existing system while keeping it running
  - **Anti-Corruption Layer:** Insert an adapter layer so new and old systems coexist
  - **Branch by Abstraction:** Extract an interface, run old and new implementations in parallel, switch when ready
  - **Parallel Run:** Run old and new systems simultaneously and compare outputs for confidence
  - **Big Bang Replacement:** Replace the entire system in one release (high risk — use with care)
- **Constraint-Aware Ideation:** After unconstrained brainstorming, filter ideas through integration constraints from Phase 0
- **Cost of Change Assessment:** Each idea cluster should be annotated with estimated migration complexity (Low / Medium / High)

**Key Activities:**
- Unconstrained ideation using HMW questions from Method 3
- Introduce brownfield solution patterns as secondary brainstorming prompts
- Convergence: prioritize ideas by user value AND migration feasibility
- Annotate top ideas with migration approach (Strangler Fig, Big Bang, etc.)

**Brownfield-Specific Artifacts:**
- `method-04-ideas.md` — Raw brainstorming output
- `method-04-convergence.md` — Prioritized ideas with migration pattern annotation

**Prompts:**
```
/dt-method-04-ideation
/dt-method-04-convergence
```

---

### Method 5: User Concepts

**Goal:** Visual concept validation — with explicit migration strategy options per concept.

**Brownfield Additions:**

- **Dual-Track Concept Cards:** Each concept card includes:
  1. The future-state user experience (standard)
  2. The migration experience — what happens to existing users during the transition?
- **Migration Strategy Options:** For each concept, articulate the migration approach:
  - What breaks for existing users, if anything?
  - How long does the transition period last?
  - What rollback option exists if the concept fails?
- **Stakeholder Acceptance Criteria:** Include the existing system owners as evaluators — "would the ops team accept this transition plan?"

**Key Activities:**
- Develop 2–3 concept descriptions from top ideas
- For each concept, define the future-state user experience AND the migration experience
- Validate concepts against both user needs and integration constraints
- Compare and evaluate concepts — include migration risk as an evaluation dimension

**Brownfield-Specific Artifacts:**
- `method-05-concept-cards.md` — Concept cards with migration strategy included

**Prompts:**
```
/dt-method-05-concepts
/dt-method-05-evaluation
```

---

### Method 6: Low-Fidelity Prototypes

**Goal:** Discover constraints through rapid prototyping — focused on integration points, not just UX.

**Brownfield Additions:**

- **Integration Spike Prototypes:** Beyond paper mockups, brownfield lo-fi prototypes often include technical spikes — small experiments to validate whether a key integration is feasible before committing to the concept.
- **Migration Prototype:** Prototype the data migration or system switchover, not just the end-state UX. Where are the failure modes?
- **Backward Compatibility Testing:** Prototype how the new concept behaves when called by existing consumers using the old interface.
- **Rollback Plan Prototype:** What does "undo" look like if we deploy the concept and it fails?

**Key Activities:**
- Build quick prototypes targeting integration boundaries (not just UI)
- Run technical spikes on highest-risk integration points
- Test hypotheses about feasibility AND migration safety
- Gather feedback from both end users AND system operators

**Brownfield-Specific Artifacts:**
- `method-06-prototype-plan.md` — Prototype scope including integration spike plan
- `method-06-test-results.md` — Feedback including operator feedback on migration safety

**Prompts:**
```
/dt-method-06-building
/dt-method-06-planning
/dt-method-06-testing
```

**Space Handoff:**
```
/dt-handoff-solution-space
```

---

## Implementation Space

### Method 7: High-Fidelity Prototypes

**Goal:** Technical feasibility testing with production-quality prototypes — running against the real system.

**Brownfield Additions:**

- **Real Integration Testing:** Hi-fi prototypes in brownfield projects should connect to the actual existing system (or a production-like replica), not just mocks.
- **Performance Regression Guard:** Establish performance baselines from the existing system and validate that the prototype does not regress key metrics.
- **Shadow Mode Deployment:** Where possible, deploy the prototype in "shadow mode" — receives real traffic but does not serve responses. Compare behavior against existing system.
- **Canary Rollout Plan:** Define what a 1% → 10% → 100% canary rollout looks like for this system.

**Brownfield-Specific Artifacts:**
- `method-07-prototype-plan.md` — Real integration scope, performance baselines
- `method-07-integration-test-results.md` — Results from testing against actual system
- `method-07-canary-plan.md` *(brownfield addition)* — Canary rollout strategy

---

### Method 8: User Testing

**Goal:** Systematic validation — including change management for existing users.

**Brownfield Additions:**

- **Change Management Testing:** Test not just the new experience, but how existing users react to the transition. Are there workflows they relied on that no longer exist?
- **Rollback Trigger Definition:** Define the specific conditions under which the team would roll back the new solution. Test that rollback works before full rollout.
- **Operations Team Acceptance Testing:** The ops team must validate that the new system is as operable (monitorable, diagnosable, deployable) as the old one.
- **Data Integrity Validation:** If data was migrated, validate that the migrated data produces the same outputs as the source system on a representative sample.

**Brownfield-Specific Artifacts:**
- `method-08-test-plan.md` — Includes change management testing and rollback criteria
- `method-08-test-results.md` — Includes ops team feedback and data integrity validation
- `method-08-rollback-criteria.md` *(brownfield addition)* — Explicit rollback decision triggers

---

### Method 9: Iteration at Scale

**Goal:** Continuous optimization and preparation for final handoff — with explicit migration path closure.

**Brownfield Additions:**

- **Migration Path Closure:** Define the end state for the old system:
  - When is the old system decommissioned?
  - Who is responsible for decommission?
  - What data archival is required before decommission?
- **Technical Debt Resolution Tracking:** Measure which items from the Technical Debt Map (Phase 0) have been resolved by the new system.
- **Operational Handoff:** Ensure the operations team has runbooks, monitoring dashboards, and incident playbooks for the new system before the old one is shut down.
- **Lessons Learned:** Document what was learned about the existing system that was not known before the DT process began.

**Brownfield-Specific Artifacts:**
- `method-09-iteration-plan.md` — Includes decommission timeline and debt resolution tracking
- `method-09-migration-closure.md` *(brownfield addition)* — Decommission plan, data archival, operational handoff
- `method-09-lessons-learned.md` *(brownfield addition)* — Brownfield discoveries and institutional knowledge preservation

**Space Handoff:**
```
/dt-handoff-implementation-space
```

---

## Non-Linear Iteration in Brownfield

Brownfield projects have the same non-linear iteration as greenfield, plus additional brownfield-specific triggers for moving backward:

| Trigger | Return To |
|---|---|
| Integration spike reveals a constraint was wrong | Method 1 (re-scope) |
| User testing reveals a critical existing workflow was missed | Method 2 (more research) |
| Migration prototype reveals unexpected data quality issues | Method 3 (re-synthesize: keep/fix/replace reclassification) |
| Hi-fi prototype fails performance regression | Method 4 (re-ideate with tighter constraints) |
| Change management testing reveals user rejection of transition | Method 5 (redesign migration experience) |
| Canary rollout reveals production-only failure | Method 6 (lo-fi prototype the failure mode) |

---

## Session Management

Same prompts as the greenfield scaffold:

```
# Start brownfield project
/dt-start-project project-slug=my-brownfield-project context="..." industry=domain project-type=brownfield

# Resume
/dt-resume-coaching project-slug=my-brownfield-project

# Advance methods
/dt-method-next

# Generate deliverables
/dt-canonical-deck
/dt-figma-export

# Hand off to implementation
# Use the "Hand off to RPI" button in DT Coach
```

---

## Progressive Hint Engine (Brownfield Additions)

The 4-level escalation from the greenfield framework applies, with brownfield-specific hints added at each level:

| Level | Style | Greenfield Example | Brownfield Addition |
|---|---|---|---|
| 1 | Broad direction | "What else did they mention?" | "What do the support tickets say about this area?" |
| 2 | Contextual focus | "You're on the right track with X. What about Y?" | "The ops team mentioned something similar — what did they say about deployment risk?" |
| 3 | Specific area | "They mentioned [topic]. What challenges might that create?" | "The integration constraint doc flagged [interface]. How does your concept handle that?" |
| 4 | Direct detail | Specific quotes or details (last resort) | Specific Phase 0 artifact content (last resort) |
