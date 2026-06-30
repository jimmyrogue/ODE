# ODE Architecture

---

# Overview

ODE introduces a control layer above planning and execution.

```text
User Input
        │
        ▼
Objective Loop
        │
 ┌──────┴──────────────┐
 │                     │
Objective State    Decision Engine
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

## Decision Filter

The central controller.

Possible decisions:

- Continue
- Stop
- Revise Design
- Update Objective
- Rollback
- Ask User

Every major decision passes through this module.

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
Decision
      │
      ▼
Objective Update
      │
      └───────────────► next iteration
```

---

# Extensibility

Each module should remain independent.

Future implementations may replace prompt-based modules with:

- sub agents
- MCP tools
- external evaluators
- learned objective models

without changing the overall architecture.