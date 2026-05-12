# RPI Guide — Brownfield Research, Plan, Implement, Review

After completing the brownfield Design Thinking workshop, the next step is the **RPI (Research → Plan → Implement → Review)** workflow from [HVE Core](https://github.com/microsoft/hve-core). For brownfield projects, RPI has a distinct character: implementation tasks are primarily **migration tasks** — strangling, extending, replacing, or migrating parts of an existing system.

See the [Greenfield RPI Guide](../rpi-guide.md) for the baseline RPI workflow. This guide documents the brownfield-specific additions and adaptations.

---

## How Brownfield DT Outputs Feed Into RPI

The brownfield DT process produces three types of input for RPI that greenfield projects do not have:

| DT Artifact | How It Feeds Into RPI |
|---|---|
| `system-inventory.md` (Phase 0) | Task Researcher uses this as the map of what exists — what to keep, what to investigate, what to avoid touching |
| `technical-debt-map.md` (Phase 0) | Task Planner uses this to identify which tasks are migration work vs. net-new work |
| `integration-constraints.md` (Phase 0) | Task Implementor uses this as a hard constraint list — interfaces that must not break |
| `method-03-keep-fix-replace.md` | Defines the scope boundary for RPI: what is in scope (fix/replace) and what is out of scope (keep) |
| `method-05-concept-cards.md` | Contains the chosen migration strategy (Strangler Fig, Big Bang, etc.) — this drives the implementation approach |
| `method-07-canary-plan.md` | Task Planner uses this to structure the rollout phases as plan checkpoints |
| `method-08-rollback-criteria.md` | Task Reviewer validates that rollback capability exists before marking review complete |
| `method-09-migration-closure.md` | Decommission tasks become the final RPI implementation tasks |

---

## Step 1: Generate the Brownfield DT Handoff Contract

In Copilot Chat, with DT Coach active:

```
/dt-handoff-implementation-space
```

The `dt-rpi-handoff-contract` instruction converts your brownfield DT artifacts into a migration-aware RPI work contract. Verify that the output contract includes:

- The chosen migration strategy (e.g., Strangler Fig, Anti-Corruption Layer)
- The Keep/Fix/Replace classification from Method 3
- Integration constraints that all implementation tasks must respect
- Acceptance criteria from Methods 7–8, including rollback conditions
- The decommission plan from Method 9

If any of these are missing, return to the DT workshop and complete the relevant artifact before proceeding.

---

## Step 2: Research (Brownfield-Specific)

```
/task-research <topic>
```

Or select **Task Researcher** from the agent picker.

### What to research for brownfield

Brownfield research has two tracks that are different from greenfield. You can cover both tracks in a single `/task-research` run by combining both prompts below, or run them as two separate sessions (use `/clear` between them) if the scope is large enough to warrant separate research documents.

**Track A: Existing System Investigation**

```
I've completed a brownfield DT workshop for [project name]. The chosen migration strategy
is [Strangler Fig / ACL / Branch by Abstraction / etc.].
The system inventory is at .copilot-tracking/dt/{slug}/system-inventory.md.
The integration constraints are at .copilot-tracking/dt/{slug}/integration-constraints.md.

Please investigate the existing codebase to understand:
1. The exact entry points and interfaces that must remain backward-compatible
2. The data models that need to be migrated, preserved, or both
3. The current test coverage and test infrastructure for the components being changed
4. Any hidden dependencies not captured in the system inventory (static analysis, grep)
5. The existing deployment and rollback mechanisms
```

**Track B: New Solution Architecture**

```
Given the system investigation above, research:
1. What new patterns, libraries, or frameworks the solution concept requires
2. How the Anti-Corruption Layer / Strangler Fig interface should be structured
3. Any external service integrations required by the new solution
4. Performance benchmarks and SLAs to match or exceed from the existing system
```

### Brownfield research outputs

In addition to standard research findings, Task Researcher should document:

- **Interface contracts** — the exact API signatures, data formats, or protocols that must be preserved
- **Data migration risks** — any data quality issues, schema incompatibilities, or transformation complexity
- **Hidden dependencies** — integrations not in the system inventory discovered during investigation
- **Rollback feasibility** — whether rollback is technically safe at each planned rollout stage

---

## Step 3: Plan (Brownfield-Specific)

```
/task-plan
```

Or select **Task Planner** from the agent picker.

### How brownfield plans differ

A brownfield implementation plan should structure tasks in phases that match the migration strategy:

**Strangler Fig plan structure:**

```
Phase 1: Build the strangler facade (backward-compatible routing layer)
  ☐ Task 1.1 — Create new interface matching existing contract
  ☐ Task 1.2 — Route 0% of traffic to new implementation (dark launch)
  ☐ Task 1.3 — Validate existing tests still pass
Phase 2: Implement new behavior behind facade
  ☐ Task 2.1 — Implement new logic
  ☐ Task 2.2 — Add parity tests (new vs. old output comparison)
  ☐ Task 2.3 — Performance baseline verification
Phase 3: Canary rollout
  ☐ Task 3.1 — Route 1% of traffic to new implementation
  ☐ Task 3.2 — Monitor and validate (canary criteria from method-07-canary-plan.md)
  ☐ Task 3.3 — Expand to 10%, then 100%
Phase 4: Decommission old implementation
  ☐ Task 4.1 — Remove old code path after 100% cutover confirmed stable
  ☐ Task 4.2 — Archive old data per decommission plan
  ☐ Task 4.3 — Update documentation and runbooks
```

Provide Task Planner with the canary plan and rollback criteria explicitly:

```
Create an implementation plan based on:
- Research: .copilot-tracking/research/YYYY-MM-DD-<topic>-research.md
- Migration strategy: [Strangler Fig / ACL / etc.] from DT concept cards
- Canary rollout plan: .copilot-tracking/dt/{slug}/method-07-canary-plan.md
- Rollback criteria: .copilot-tracking/dt/{slug}/method-08-rollback-criteria.md
- Integration constraints: .copilot-tracking/dt/{slug}/integration-constraints.md

Structure the plan with phase checkpoints so I can validate before proceeding
to the next migration phase.
```

---

## Step 4: Implement (Brownfield-Specific)

```
/task-implement
```

Or select **Task Implementor** from the agent picker.

### Brownfield implementation guard rails

Before starting each phase, explicitly remind Task Implementor of the constraints:

```
Implement Phase 1 from .copilot-tracking/plans/YYYY-MM-DD-<topic>-plan.md.

BROWNFIELD CONSTRAINTS (must be respected at all times):
- Do NOT break these interfaces: [list from integration-constraints.md]
- Do NOT modify these components (Keep list): [list from method-03-keep-fix-replace.md]
- All existing tests must continue to pass after each task
- The rollback criterion is: [from method-08-rollback-criteria.md]

Start with Task 1.1.
```

### Implementation checkpoints

After each phase, before proceeding:

1. Run existing tests — they must all pass
2. Verify the interface contract is intact (backward compatibility check)
3. Confirm rollback is safe (the old path still works)

Do not proceed to the next phase until these checks pass.

---

## Step 5: Review (Brownfield-Specific)

```
/task-review
```

Or select **Task Reviewer** from the agent picker.

### Brownfield review criteria

In addition to standard review checks, Task Reviewer must validate:

```
Review the brownfield migration implementation against:
- Research: .copilot-tracking/research/YYYY-MM-DD-<topic>-research.md
- Plan: .copilot-tracking/plans/YYYY-MM-DD-<topic>-plan.md
- Changes: .copilot-tracking/changes/YYYY-MM-DD-<topic>-changes.md
- Integration constraints: .copilot-tracking/dt/{slug}/integration-constraints.md
- Rollback criteria: .copilot-tracking/dt/{slug}/method-08-rollback-criteria.md

For this brownfield migration, also validate:
1. All non-negotiable interfaces are still intact (from integration-constraints.md)
2. Rollback capability exists and has been tested
3. Canary rollout conditions are met before proceeding to the next phase
4. No components from the "Keep" list were modified
5. Data integrity: migrated data produces equivalent outputs to the source system
6. Ops team acceptance criteria are met (runbooks, monitoring, alerts exist for new components)
```

### Brownfield review outputs

The review document should include a **migration health checklist**:

```markdown
## Migration Health Checklist

- [ ] All existing tests pass
- [ ] Non-negotiable interfaces preserved (backward compatibility confirmed)
- [ ] New behavior matches DT acceptance criteria
- [ ] Performance meets or exceeds existing system baseline
- [ ] Rollback tested and confirmed safe
- [ ] Canary criteria met for current phase
- [ ] No unintended changes to "Keep" components
- [ ] Data integrity validated (if applicable)
- [ ] Runbooks and monitoring dashboards updated for new components
```

---

## Brownfield RPI Artifact Directory Structure

```
.copilot-tracking/
├── dt/{project-slug}/                       # DT brownfield artifacts
│   ├── coaching-state.md
│   ├── system-inventory.md                  # Phase 0 — existing system map
│   ├── technical-debt-map.md                # Phase 0 — known pain points
│   ├── integration-constraints.md           # Phase 0 — non-negotiable interfaces
│   ├── method-03-keep-fix-replace.md        # Scope boundary for RPI
│   ├── method-05-concept-cards.md           # Chosen migration strategy
│   ├── method-07-canary-plan.md             # Rollout plan for RPI phases
│   ├── method-08-rollback-criteria.md       # Rollback decision triggers
│   ├── method-09-migration-closure.md       # Decommission plan
│   └── [handoff contract]                   # Generated by /dt-handoff-implementation-space (filename assigned by DT Coach)
│
├── research/
│   ├── YYYY-MM-DD-existing-system-research.md   # Track A: existing system investigation
│   └── YYYY-MM-DD-new-solution-research.md      # Track B: new solution architecture (optional separate run)
│
├── plans/
│   ├── YYYY-MM-DD-<topic>-plan.md           # Phase-structured migration plan
│   └── YYYY-MM-DD-<topic>-details.md
│
├── changes/
│   └── YYYY-MM-DD-<topic>-changes.md
│
└── reviews/
    └── YYYY-MM-DD-<topic>-review.md         # Includes migration health checklist
```

---

## Migration Pattern Reference for RPI

Use the DT Method 5 concept card to confirm which migration pattern applies, then follow the corresponding RPI structure:

| Pattern | RPI Research Focus | RPI Plan Structure | RPI Review Gate |
|---|---|---|---|
| **Strangler Fig** | Find existing entry points and routing layer | Phase by component; dark launch → canary → cutover | Each phase: old path still works |
| **Anti-Corruption Layer** | Map domain model incompatibilities | Build ACL first; new system behind ACL; migrate traffic | ACL translates correctly; both models stay consistent |
| **Branch by Abstraction** | Find all call sites of the component being replaced | Extract interface; implement new behind interface; switch | Old implementation removed after switch confirmed |
| **Parallel Run** | Understand comparison requirements and divergence tolerance | Build new system; run in parallel; compare; cut over | Output parity confirmed on representative sample |
| **Feature Flag Migration** | Find feature flag infrastructure (or build it) | Flag per feature; enable progressively; monitor | Flag debt resolved; old code paths removed |
| **Big Bang Replacement** | Complete end-to-end analysis of all existing functionality | Single coordinated cutover plan; extensive pre-validation | All acceptance tests pass; rollback plan tested |
| **Database First** | Map schema differences; data volume; transformation complexity | Schema migration; dual-write; application migration; cutover | Data integrity validated; no data loss confirmed |

---

## See Also

- [Brownfield Workshop Guide](./workshop-guide.md) — The brownfield 9-method DT framework
- [Brownfield Reference](./reference.md) — Brownfield agents, prompts, and artifact templates
- [Greenfield RPI Guide](../rpi-guide.md) — Baseline RPI workflow
- [HVE Core RPI Documentation](https://github.com/microsoft/hve-core/blob/main/docs/rpi/README.md) — Upstream reference
