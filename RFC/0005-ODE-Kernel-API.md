# RFC 0005 — ODE Kernel API

**Status:** Draft

**Author:** ODE Contributors

**Created:** 2026

**Version:** 0.2

---

# ODE Kernel API

## The Minimal Interface for Objective-Driven Runtime

---

# Abstract

RFC0004 introduced the ODE Kernel as the runtime control core of objective-driven intelligence.

This RFC defines the minimum API surface required for an implementation to be considered ODE-compatible.

The Kernel API is not tied to any programming language, model provider, agent framework, or execution engine.

It defines semantic operations.

Implementations may expose these operations as:

- functions
- prompts
- MCP tools
- HTTP APIs
- CLI commands
- SDK methods
- internal runtime calls

The API describes what an objective-driven runtime must preserve, evaluate, and evolve.

It does not prescribe how execution itself must be performed.

---

# Design Goals

The ODE Kernel API should satisfy five design goals.

## Minimal

Only define the smallest set of operations required to maintain objective-driven execution.

## Agent-Agnostic

The API should work with any execution engine.

Examples include:

- coding agents
- research agents
- browser agents
- workflow agents
- custom runtimes

## State-Oriented

Every API call should read from or write to Kernel State.

Objective continuity depends on explicit state transitions, not hidden agent behavior.

## Auditable

Every important state change should produce a traceable record.

An ODE-compatible runtime should be able to explain:

- what objective was active,
- what action was selected,
- why alternatives were rejected,
- what feedback was observed,
- and how the objective evolved.

## Loop-Compatible

The API should support continuous objective evolution.

Each loop should preserve enough state for the next loop to deliberate, execute, evaluate, and improve.

---

# Non-Goals

This RFC does not define:

- a TypeScript SDK,
- a Python package,
- an HTTP protocol,
- an MCP schema,
- a storage engine,
- a prompt format,
- or a specific execution engine.

Those may be defined in later implementation RFCs.

RFC0005 only defines the semantic API boundary.

---

# Kernel Boundaries

The Kernel owns objective continuity.

The execution engine owns domain execution.

The Kernel may delegate action.

The Kernel must not delegate purpose.

This boundary is the central separation in ODE-compatible systems.

Execution engines may decide how to perform a domain action.

The Kernel decides whether that action remains aligned with the objective, whether the objective has drifted, and how the objective should evolve after feedback.

---

# Core Kernel State

The Kernel maintains one runtime state.

The exact representation is implementation-specific, but an ODE-compatible runtime should preserve the following conceptual structure.

```yaml
kernel_state:
  kernel_id:
  version:
  runtime_mode:
  loop_count:

  objective_state:
    current_objective:
    objective_function:
    confidence:
    assumptions:
    constraints:
    metrics:
    lineage:

  deliberation_state:
    candidate_actions:
    selected_action:
    rejected_actions:
    decision_reason:
    commitment:
    refusal_reason:

  execution_state:
    plan:
    actions_taken:
    result:

  feedback_state:
    observations:
    metrics:
    errors:
    confidence:

  evaluation_state:
    alignment_score:
    drift_detected:
    progress:
    objective_report:

  memory:
    objective_memory:
    decision_memory:
    feedback_memory:
```

Kernel State is the continuity layer.

Execution engines may be stateless.

The Kernel must not be.

---

# Kernel API Overview

The complete Kernel API consists of fourteen semantic operations.

```text
initializeKernel()
loadObjective()
discoverObjective()
formalizeObjective()
enterDeliberation()
selectAction()
createDesign()
commitExecution()
submitFeedback()
evaluateObjective()
updateObjective()
persistMemory()
nextLoop()
terminateKernel()
```

Not every implementation must expose every operation publicly.

However, an ODE-compatible runtime must preserve the semantics of the required operations defined later in this RFC.

---

# API Definitions

---

## 1. initializeKernel

Purpose

Create a new ODE Kernel runtime state.

Signature

```text
initializeKernel(input: KernelInitInput): KernelState
```

Input

```yaml
input:
  user_request:
  context:
  existing_memory:
  constraints:
```

Output

```yaml
kernel_state:
  kernel_id:
  runtime_mode: initialized
  loop_count: 0
```

Notes

`initializeKernel` creates runtime state.

It does not yet prove that the system understands the objective.

That responsibility belongs to `loadObjective`, `discoverObjective`, and `formalizeObjective`.

---

## 2. loadObjective

Purpose

Load existing Objective Memory into the current runtime.

Signature

```text
loadObjective(kernel_state, memory): KernelState
```

Responsibilities

- load current objective
- load objective lineage
- load previous decisions
- load known constraints
- load known objective drift events

Output

```yaml
objective_state:
  current_objective:
  lineage:
  confidence:
  assumptions:
  constraints:
```

Notes

`loadObjective` is required whenever objective memory exists.

An ODE-compatible runtime should not begin deliberation from a blank objective state when prior objective memory is available.

---

## 3. discoverObjective

Purpose

Infer the real objective behind the input.

Signature

```text
discoverObjective(kernel_state, input): ObjectiveCandidate
```

Output

```yaml
objective_candidate:
  raw_request:
  inferred_objective:
  user_value:
  success_definition:
  assumptions:
  anti_goals:
  confidence:
```

Notes

`discoverObjective` is especially important when the user provides a surface task but the underlying objective is broader.

Example:

```text
Surface task:
Fix this bug.

Possible objective:
Restore user trust in a critical workflow without introducing regressions.
```

The Kernel should preserve the inferred objective separately from the raw request.

---

## 4. formalizeObjective

Purpose

Convert the discovered objective into an objective function.

Signature

```text
formalizeObjective(objective_candidate): ObjectiveFunction
```

Output

```yaml
objective_function:
  primary_objective:
  secondary_objectives:
  metrics:
    - name:
      direction:
      proxy:
      confidence:
  constraints:
  tradeoffs:
```

Notes

An objective function does not need to be mathematical.

It must be explicit enough for the runtime to evaluate whether later actions moved the system closer to or farther from the objective.

---

## 5. enterDeliberation

Purpose

Enter Deliberation Mode before execution.

Signature

```text
enterDeliberation(kernel_state): DeliberationState
```

Responsibilities

- load objective state
- inspect memory
- generate candidate actions
- estimate objective contribution
- reject low-value actions

Output

```yaml
deliberation_state:
  candidate_actions:
    - action:
      expected_contribution:
      complexity_cost:
      risk_cost:
      reversibility:
      evidence_quality:
  rejected_actions:
    - action:
      reason:
```

Notes

Deliberation is not planning.

Planning answers how to execute.

Deliberation decides whether an action deserves execution.

---

## 6. selectAction

Purpose

Select the next best action.

Signature

```text
selectAction(deliberation_state): Decision
```

Suggested scoring

```text
Action Score =
  Objective Contribution
  - Complexity Cost
  - Risk Cost
  - Runtime Cost
  - Token Cost
  - Maintenance Cost
```

Output

```yaml
decision:
  decision_type:
  selected_action:
  reason:
  expected_objective_contribution:
  known_risks:
  rejected_alternatives:
  required_evidence:
  reconsideration_conditions:
  confidence:
```

Notes

The exact scoring method is implementation-specific.

`decision_type` should support at least:

- execute
- refuse
- defer
- gather_more_evidence
- update_objective

The invariant is that the decision must be justified in relation to the current objective.

If the decision is `execute`, the selected action must produce a commitment record.

If the decision is not `execute`, the refusal or deferral reason must be preserved.

---

## 7. createDesign

Purpose

Convert the selected action into an executable design.

Signature

```text
createDesign(decision): Design
```

Output

```yaml
design:
  strategy:
  execution_plan:
  files_to_change:
  tools_required:
  validation_plan:
```

Notes

`createDesign` belongs between deliberation and execution.

It converts a justified decision into an executable plan while preserving the objective rationale.

---

## 8. commitExecution

Purpose

Record that execution has occurred.

The Kernel does not execute directly.

Execution is performed by an external execution engine.

Signature

```text
commitExecution(kernel_state, execution_result): KernelState
```

Input

```yaml
execution_result:
  actions_taken:
  changed_files:
  commands_run:
  result:
  notes:
```

Output

```yaml
execution_state:
  result:
  actions_taken:
  artifacts:
```

Notes

The Kernel may delegate execution.

It must still record what happened.

---

## 9. submitFeedback

Purpose

Submit observable evidence after execution.

Signature

```text
submitFeedback(kernel_state, feedback): KernelState
```

Input

```yaml
feedback:
  tests:
  logs:
  metrics:
  user_feedback:
  screenshots:
  runtime_observations:
  errors:
```

Output

```yaml
feedback_state:
  observations:
  metrics:
  errors:
  confidence:
```

Notes

Feedback is evidence.

It is not yet judgment.

Judgment belongs to `evaluateObjective`.

---

## 10. evaluateObjective

Purpose

Evaluate whether execution moved the system closer to the objective.

Signature

```text
evaluateObjective(kernel_state): ObjectiveEvaluation
```

Output

```yaml
evaluation:
  alignment_score:
  objective_progress:
  surface_task_completed:
  real_objective_progress:
  objective_drift:
  analysis:
  evidence:
```

Notes

An execution can complete the surface task while failing the real objective.

Example:

```text
Surface task completed:
The requested feature was implemented.

Real objective failed:
The implementation increased complexity, reduced reliability, and made future evolution harder.
```

`evaluateObjective` exists to make that distinction explicit.

---

## 11. updateObjective

Purpose

Update the objective state when justified by evidence.

Signature

```text
updateObjective(kernel_state, evaluation): KernelState
```

Possible updates

- refine objective
- adjust confidence
- update assumptions
- update metrics
- append lineage
- mark drift
- preserve current objective

Output

```yaml
objective_update:
  previous_objective:
  updated_objective:
  reason:
  evidence:
  confidence_delta:
```

Notes

Objective updates must be versioned.

The Kernel should never silently overwrite the previous objective.

---

## 12. persistMemory

Purpose

Persist long-term objective memory.

Signature

```text
persistMemory(kernel_state): ObjectiveMemory
```

Output

```yaml
objective_memory:
  current_objective:
  objective_lineage:
  transition_history:
  decision_history:
  feedback_summary:
  drift_events:
```

Notes

If memory is not persisted, the next loop cannot inherit objective continuity.

For ODE, forgetting why is a runtime failure.

---

## 13. nextLoop

Purpose

Advance the Kernel to the next loop.

Signature

```text
nextLoop(kernel_state): KernelState
```

Rules

- increment loop count
- load latest objective state
- re-enter deliberation
- do not skip evaluation
- do not skip memory persistence

Output

```yaml
kernel_state:
  loop_count:
  runtime_mode:
  objective_state:
  memory:
```

Notes

`nextLoop` is not a reset.

It is a continuation.

---

## 14. terminateKernel

Purpose

Terminate the current objective loop.

Termination does not delete Objective Memory.

Signature

```text
terminateKernel(kernel_state, reason): KernelFinalState
```

Output

```yaml
final_state:
  status:
  final_objective:
  final_alignment_score:
  objective_report:
  memory_persisted:
  reason:
```

Notes

Termination ends a runtime loop.

It should preserve enough information for future agents or runtimes to understand the final objective state.

---

# Required Runtime Invariants

An implementation is ODE-compatible only if it satisfies these invariants.

## Invariant 1

Execution must not occur before Deliberation.

## Invariant 2

Every execution must produce feedback.

## Invariant 3

Every feedback must trigger evaluation.

## Invariant 4

Every objective update must be persisted.

## Invariant 5

Objectives must be versioned, not overwritten.

## Invariant 6

The Kernel may delegate execution, but must not delegate objective continuity.

## Invariant 7

Deliberation must be able to produce a non-execution decision.

An ODE-compatible runtime must preserve why an action was refused, deferred, or blocked on missing evidence.

---

# Minimal ODE-Compatible Runtime

A minimal implementation must support the following operations:

```text
initializeKernel()
loadObjective()
enterDeliberation()
selectAction()
commitExecution()
submitFeedback()
evaluateObjective()
updateObjective()
persistMemory()
nextLoop()
```

These operations form the irreducible objective loop.

Optional but recommended operations:

```text
discoverObjective()
formalizeObjective()
createDesign()
terminateKernel()
```

An implementation may combine optional operations internally.

It must not skip the required semantics.

---

# Example Flow

```text
initializeKernel
      ↓
loadObjective
      ↓
discoverObjective
      ↓
formalizeObjective
      ↓
enterDeliberation
      ↓
selectAction
      ↓
createDesign
      ↓
external execution engine acts
      ↓
commitExecution
      ↓
submitFeedback
      ↓
evaluateObjective
      ↓
updateObjective
      ↓
persistMemory
      ↓
nextLoop
```

The flow may be implemented through functions, prompts, tools, APIs, or internal runtime calls.

The semantic order must remain intact.

---

# Compatibility Statement

An ODE-compatible runtime must expose or internally preserve the Kernel API semantics defined in this RFC.

It may choose any implementation language.

It may use any model provider.

It may delegate execution to any agent.

It must maintain objective continuity across loops.

---

# Closing Statement

The ODE Kernel API defines the boundary between execution engines and objective-driven control.

Execution engines answer:

> How do I act?

The Kernel API answers:

> How do I preserve, evaluate, and evolve why I act?

RFC0005 deliberately stops at the semantic API level.

Later implementation work may map these operations into concrete modules such as:

```text
runtime/
  kernel.ts
  state.ts
  memory.ts
  deliberation.ts
  evaluation.ts
```

The API comes first.

The SDK should grow from it.
