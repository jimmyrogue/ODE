# ODE Architecture

---

# Overview

ODE introduces a control layer above planning and execution.

```text
User Input
        │
        ▼
Objective Memory
        │
        ▼
Objective Loop
        │
 ┌──────┴──────────────┐
 │                     │
Objective State    Deliberation
 │                     │
 └──────┬──────────────┘
        ▼
Sub Skills
        ▼
Execution Agent
        ▼
Environment
        ▼
Feedback
        ▼
Objective Loop
```

---

# Components

## Objective Memory

Purpose:

Preserve objective history across time, agents, and implementations.

Output:

- objective lineage
- decision history
- rejected alternatives
- validated assumptions
- objective drift records

---

## Objective Discovery

Purpose:

Infer the real objective behind the user's request.

Output:

- inferred objective
- assumptions
- anti-goals

---

## Objective Formalization

Converts objectives into measurable functions.

Produces:

- objective function
- metrics
- constraints
- trade-offs

---

## Deliberation

Purpose:

Evaluate candidate actions before execution.

Deliberation decides whether an action deserves to proceed into design and execution.

Decision Filter is an internal part of Deliberation, responsible for choosing among candidate actions.

Possible decisions:

- Continue
- Stop
- Revise Design
- Update Objective
- Rollback
- Ask User

---

## Design Generator

Produces candidate solutions.

Each solution includes:

- expected contribution
- estimated cost
- estimated risk

---

## Execution Runner

Delegates work to the underlying execution engine.

Possible engines:

- Claude Code
- Codex
- Cursor
- Kiro
- Local Runtime

ODE does not execute code itself.

---

## Feedback Collector

Collects every available signal.

Examples:

- tests
- logs
- screenshots
- runtime metrics
- benchmarks
- user feedback

---

## Objective Evaluator

Compares:

Current State

vs

Desired Objective

Outputs:

- alignment score
- progress
- drift
- observations

---

## Objective Updater

Updates the objective only when justified by evidence.

The objective is treated as persistent state.

---

# State

ODE maintains a long-lived Objective State.

```yaml
objective_state:

objective:

objective_function:

current_design:

feedback_history:

evaluation_history:

decision_history:

loop_count:
```

Each iteration reads from and writes to this state.

---

# Data Flow

```text
Objective
      │
      ▼
Deliberation
      │
      ▼
Design
      │
      ▼
Execution
      │
      ▼
Feedback
      │
      ▼
Evaluation
      │
      ▼
Objective Update
      │
      └───────────────► next iteration
```

---

# Runtime Modes

ODE agents operate through several modes.

## Objective Mode

Discover and formalize the current objective.

---

## Deliberation Mode

Evaluate candidate actions before execution.

---

## Execution Mode

Perform the selected action.

---

## Feedback Mode

Collect observable evidence.

---

## Evaluation Mode

Measure progress toward the objective.

---

## Update Mode

Refine objective state and memory.

---

# Extensibility

Each module should remain independent.

Future implementations may replace prompt-based modules with:

- sub agents
- MCP tools
- external evaluators
- learned objective models

without changing the overall architecture.
