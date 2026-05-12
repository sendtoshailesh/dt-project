# Reference — Brownfield Agents, Prompts & Artifacts

Complete reference for the brownfield SDLC Design Thinking scaffold. This extends the [greenfield reference](../reference.md) with brownfield-specific additions.

---

## Agents

The same agents from the greenfield scaffold apply. The `project-type=brownfield` parameter in `/dt-start-project` signals brownfield coaching mode to DT Coach.

| Agent | Description |
|---|---|
| **DT Coach** | Primary coaching agent — applies brownfield-aware coaching when `project-type=brownfield` is set |
| **Task Researcher** (via handoff) | Research, Planning, and Implementation agent for the technical migration work that follows DT |

---

## Prompts

### Project Lifecycle

| Prompt | Greenfield | Brownfield Usage |
|---|---|---|
| `/dt-start-project` | Initialize new DT project | Add `project-type=brownfield` and `existing-system="..."` parameters |
| `/dt-resume-coaching` | Resume previous session | Same — brownfield context is restored from coaching state |
| `/dt-method-next` | Advance to next method | Same |

### Brownfield Start Command

```
/dt-start-project \
  project-slug=my-brownfield-project \
  context="Problem statement describing what is broken or needs to change" \
  industry=your-industry \
  project-type=brownfield \
  existing-system="Brief description: tech stack, age, user count, key pain points"
```

### Method-Specific (same as greenfield)

| Prompt | Method | Description |
|---|---|---|
| `/dt-method-04-ideation` | 4 | Divergent ideation — brownfield patterns available as framing lenses |
| `/dt-method-04-convergence` | 4 | Convergence and voting — includes migration feasibility as a dimension |
| `/dt-method-05-concepts` | 5 | Concept development — dual-track (future UX + migration experience) |
| `/dt-method-05-evaluation` | 5 | Concept comparison — migration risk is an evaluation dimension |
| `/dt-method-06-building` | 6 | Prototype building — includes integration spike planning |
| `/dt-method-06-planning` | 6 | Prototype planning |
| `/dt-method-06-testing` | 6 | Prototype testing — includes backward compatibility and rollback testing |

### Handoffs & Deliverables (same as greenfield)

| Prompt | Description |
|---|---|
| `/dt-handoff-problem-space` | Summarize Problem Space (Methods 1-3) findings — brownfield coaching state includes Phase 0 artifacts |
| `/dt-handoff-solution-space` | Summarize Solution Space (Methods 4-6) outcomes — includes migration strategy summary |
| `/dt-handoff-implementation-space` | Transition to implementation — includes decommission plan |
| `/dt-canonical-deck` | Generate canonical presentation deck |
| `/dt-figma-export` | Export artifacts to FigJam board |

---

## Artifact Storage

All artifacts (greenfield + brownfield-specific) are stored under `.copilot-tracking/dt/{project-slug}/`.

### Phase 0 Artifacts (Brownfield-Specific)

| Artifact | Description |
|---|---|
| `system-inventory.md` | Existing system components, user groups, integrations, data assets |
| `technical-debt-map.md` | Known pain points, operational debt, impact assessment, hard constraints |
| `integration-constraints.md` | Non-negotiable interfaces, data migration constraints, infrastructure constraints |

### Method Artifacts

#### Method 1: Scope Conversations

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-01-stakeholder-map.md` | Stakeholder map | Includes existing system owners and operations team |
| `method-01-scope-summary.md` | Scope definition and problem framing | Includes current-state baseline metrics |
| `method-01-constraint-validation.md` | _(new in brownfield)_ | Which Phase 0 constraints survived stakeholder scrutiny |

#### Method 2: Design Research

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-02-research-plan.md` | Interview and observation plan | Includes system archaeology and ops interview plan |
| `method-02-interview-notes.md` | Structured interview findings | Includes ops team and support team findings |
| `method-02-current-journey-map.md` | _(new in brownfield)_ | As-is user journey through existing system with pain annotations |

#### Method 3: Input Synthesis

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-03-themes.md` | Thematic clusters | Includes Keep/Fix/Replace categorization |
| `method-03-hmw-questions.md` | How Might We questions | Constraint-aware HMW questions |
| `method-03-keep-fix-replace.md` | _(new in brownfield)_ | Explicit inventory of what to preserve, fix, and retire |

#### Method 4: Brainstorming

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-04-ideas.md` | Raw brainstorming output | Same |
| `method-04-convergence.md` | Prioritized and clustered ideas | Includes migration pattern annotation (Strangler Fig, etc.) |

#### Method 5: User Concepts

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-05-concept-cards.md` | Concept descriptions and cards | Includes migration experience and rollback option per concept |

#### Method 6: Low-Fidelity Prototypes

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-06-prototype-plan.md` | Prototype scope and hypotheses | Includes integration spike plan |
| `method-06-test-results.md` | Feedback and constraint findings | Includes operator feedback and backward compatibility results |

#### Method 7: High-Fidelity Prototypes

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-07-prototype-plan.md` | Hi-fi prototype plan | Includes real integration scope and performance baselines |
| `method-07-integration-test-results.md` | _(new in brownfield)_ | Results from testing against actual existing system |
| `method-07-canary-plan.md` | _(new in brownfield)_ | Canary rollout strategy (1% → 10% → 100%) |

#### Method 8: User Testing

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-08-test-plan.md` | Test plan | Includes change management testing and rollback criteria |
| `method-08-test-results.md` | Test results | Includes ops team acceptance and data integrity validation |
| `method-08-rollback-criteria.md` | _(new in brownfield)_ | Explicit conditions that trigger rollback |

#### Method 9: Iteration at Scale

| Artifact | Greenfield | Brownfield Addition |
|---|---|---|
| `method-09-iteration-plan.md` | Iteration and scaling plan | Includes decommission timeline and debt resolution tracking |
| `method-09-migration-closure.md` | _(new in brownfield)_ | Decommission plan, data archival, operational handoff |
| `method-09-lessons-learned.md` | _(new in brownfield)_ | Brownfield discoveries and institutional knowledge preservation |

---

## Brownfield Solution Patterns Reference

Use these patterns as framing lenses during Method 4 (Brainstorming) and Method 5 (User Concepts):

| Pattern | Description | When to Use | Key Risk |
|---|---|---|---|
| **Strangler Fig** | Gradually replace existing system piece by piece while it remains in production | Most brownfield modernization; low disruption tolerance | Long coexistence period increases complexity |
| **Anti-Corruption Layer** | Insert an adapter between old and new system to translate between their models | New and old systems have incompatible domain models | Adapter becomes permanent and accumulates debt |
| **Branch by Abstraction** | Extract an interface, run old and new implementations behind it, switch when ready | Replacing a single component within a larger system | Requires discipline to remove the old implementation |
| **Parallel Run** | Run old and new systems simultaneously; compare outputs to build confidence | Data processing, financial calculations, report generation | Operational cost of running two systems |
| **Feature Flag Migration** | New system is deployed but old behavior is default; new behavior is enabled progressively | User-facing features where individual rollback is needed | Flag management overhead; flag debt |
| **Big Bang Replacement** | Replace entire system in a single release | Small systems; hard migration deadlines; no production traffic during cutover | High risk; difficult to test fully before production |
| **Database First** | Migrate the data layer first, keep application logic on top | Data quality problems; schema migration required before feature work | Data migration complexity; dual-write period |

---

## Instructions (Auto-Loaded)

All greenfield instructions from the HVE Design Thinking extension auto-load as in the standard setup. The `project-type=brownfield` parameter in the coaching state activates brownfield-aware coaching within the existing instruction set.

See the [greenfield reference](../reference.md#instructions-43--auto-loaded) for the full instruction list.

---

## Full Brownfield Artifact Directory Structure

```
.copilot-tracking/dt/{project-slug}/
│
├── coaching-state.md                    # YAML coaching state (includes project-type: brownfield)
│
├── # Phase 0 — System Discovery (brownfield only)
├── system-inventory.md
├── technical-debt-map.md
├── integration-constraints.md
│
├── # Method 1 — Scope Conversations
├── method-01-stakeholder-map.md
├── method-01-scope-summary.md
├── method-01-constraint-validation.md   # brownfield addition
│
├── # Method 2 — Design Research
├── method-02-research-plan.md
├── method-02-interview-notes.md
├── method-02-current-journey-map.md     # brownfield addition
│
├── # Method 3 — Input Synthesis
├── method-03-themes.md
├── method-03-hmw-questions.md
├── method-03-keep-fix-replace.md        # brownfield addition
│
├── # Method 4 — Brainstorming
├── method-04-ideas.md
├── method-04-convergence.md
│
├── # Method 5 — User Concepts
├── method-05-concept-cards.md
│
├── # Method 6 — Low-Fidelity Prototypes
├── method-06-prototype-plan.md
├── method-06-test-results.md
│
├── # Method 7 — High-Fidelity Prototypes
├── method-07-prototype-plan.md
├── method-07-integration-test-results.md  # brownfield addition
├── method-07-canary-plan.md               # brownfield addition
│
├── # Method 8 — User Testing
├── method-08-test-plan.md
├── method-08-test-results.md
├── method-08-rollback-criteria.md         # brownfield addition
│
└── # Method 9 — Iteration at Scale
    ├── method-09-iteration-plan.md
    ├── method-09-migration-closure.md     # brownfield addition
    └── method-09-lessons-learned.md      # brownfield addition
```
