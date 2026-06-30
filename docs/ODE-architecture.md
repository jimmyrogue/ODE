# ODE Architecture

---

# Overview

ODE is a control architecture for objective-driven intelligent systems.

It does not replace planners, tools, models, or execution engines.

It adds a control layer that keeps those capabilities aligned with an evolving objective.

```text
User Input
    ↓
Objective Layer
    ↓
ODE Kernel
    ↓
┌──────────────────────────────────────────┐
│ Objective Memory                         │
│ Deliberation                             │
│ Objective State                          │
│ Feedback Interpretation                  │
│ Objective Update                         │
│ Objective Report                         │
└──────────────────────────────────────────┘
    ↓
Delegated Execution Engine
    ↓
Environment
    ↓
Feedback
    ↓
ODE Kernel
    ↓
Objective Memory
```

The Kernel may delegate action.

It must not delegate purpose.

---

# Architectural Boundary

ODE separates control from execution.

## ODE Owns

- objective continuity
- objective memory
- deliberation
- decision records
- drift detection
- objective evaluation
- objective updates
- objective reports

## Execution Engines Own

- coding
- research
- browsing
- tool usage
- file editing
- domain-specific implementation
- external system interaction

This boundary prevents the execution engine from becoming the source of purpose.

---

# Core Components

## Objective Layer

The Objective Layer sits above planning and execution.

It asks:

> Did this action move the system closer to the objective?

The Objective Layer is the conceptual home for Objective Memory, Deliberation, Kernel control, feedback evaluation, and Objective Reports.

---

## ODE Kernel

The Kernel is the minimal control core.

It preserves the objective loop.

It is small but opinionated.

Its invariant is:

> Action must remain accountable to an evolving objective.

The Kernel coordinates modes.

It does not perform all work itself.

---

## Objective Memory

Objective Memory preserves direction across time.

It stores:

- current objective
- objective lineage
- objective transitions
- accepted assumptions
- constraints
- decision history
- rejected alternatives
- feedback summaries
- drift events

Objective Memory is not temporary context.

Context helps the system respond.

Objective Memory helps the system continue.

---

## Deliberation

Deliberation evaluates candidate actions before execution.

It decides whether an action deserves to become real.

Possible decisions:

- execute
- refuse
- defer
- gather more evidence
- revise action
- update objective
- ask user

When Deliberation selects an action, it should produce a commitment record.

That record preserves why the action deserved execution.

---

## Design

Design converts an accepted decision into an executable plan.

Design is downstream of Deliberation.

It should preserve:

- selected action
- objective served
- expected contribution
- known risks
- validation plan
- reconsideration conditions

---

## Execution

Execution is delegated to the underlying engine.

The execution engine may be Codex, Claude Code, Cursor, Kiro, a local runtime, or another system.

Execution produces artifacts and observable changes.

It does not directly update the objective.

---

## Feedback

Feedback collects evidence from the world.

Examples:

- tests
- logs
- metrics
- benchmarks
- user feedback
- screenshots
- runtime observations

Feedback is evidence.

Evaluation turns evidence into judgment.

---

## Objective Evaluation

Evaluation compares observed reality with the active objective.

It must distinguish:

- task completion
- local success
- objective progress
- objective drift
- learning from failure

An action can succeed locally while failing the objective.

An action can fail locally while improving objective understanding.

---

## Objective Report

Every completed loop should produce an Objective Report.

The report is not a receipt for completed work.

It is the accountable trace of the objective loop.

It records:

- objective state
- execution summary
- decision summary
- evaluation
- objective evolution
- next iteration

Reports feed Objective Memory.

---

# Kernel State

ODE maintains persistent Kernel State.

```yaml
kernel_state:
  runtime_mode:
  loop_count:

  objective_state:
    current_objective:
    confidence:
    assumptions:
    constraints:
    lineage:

  deliberation_state:
    candidate_actions:
    selected_action:
    rejected_actions:
    commitment:
    refusal_reason:

  execution_state:
    plan:
    actions_taken:
    artifacts:

  feedback_state:
    observations:
    metrics:
    errors:

  evaluation_state:
    alignment_score:
    surface_success:
    objective_progress:
    drift_detected:

  memory:
    objective_memory:
    decision_memory:
    feedback_memory:

  objective_report:
```

The exact representation is implementation-specific.

The semantic state must be preserved.

---

# Data Flow

```text
Objective Memory
      ↓
Objective State
      ↓
Deliberation
      ↓
Decision / Commitment
      ↓
Design
      ↓
Execution
      ↓
Feedback
      ↓
Evaluation
      ↓
Objective Report
      ↓
Objective Memory
      ↓
Next Loop
```

The loop is complete only after the report and memory update are produced.
