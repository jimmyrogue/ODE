# RFC 0004 — ODE Kernel

**Status:** Draft

**Author:** ODE Contributors

**Created:** 2026

**Version:** 0.2

---

# ODE Kernel

## The Runtime Specification for Objective-Driven Intelligence

---

# Abstract

Previous RFCs introduced the theoretical foundations of ODE.

- RFC0001 defined Objective-Driven Evolution.
- RFC0002 introduced Objective Memory.
- RFC0003 introduced Deliberation.

This RFC introduces the **ODE Kernel**.

The ODE Kernel is the minimal control core required for an objective-driven intelligent system.

It is not an agent.

It is not a planner.

It is not a language model.

It is the control core responsible for maintaining objective continuity throughout the entire lifecycle of an intelligent system.

Just as an operating system kernel coordinates processes, memory, scheduling, and interrupts, the ODE Kernel coordinates objectives, deliberation, execution, evaluation, and evolution.

The Kernel should remain small.

It should be opinionated about one invariant:

> Action must remain accountable to an evolving objective.

---

# Motivation

Modern AI agents already possess powerful capabilities.

They can:

- reason
- plan
- execute
- use tools
- write code
- call APIs

However, these capabilities operate largely independently.

What is missing is a persistent control mechanism that continuously answers one question:

> **Are all current actions still aligned with the objective?**

ODE Kernel exists to answer that question.

---

# Design Goals

The Kernel should satisfy six requirements.

## Minimal Control Core

The Kernel should contain only the control responsibilities required to preserve the objective loop.

It should not absorb domain-specific execution, planning, tool use, or implementation details.

Smallness is a design requirement.

The Kernel must remain understandable enough to audit objective continuity.

---

## Objective Continuity

Objectives should survive individual executions.

Execution ends.

Objectives remain.

---

## Continuous Deliberation

Execution should never become autonomous without first passing through deliberation.

Every significant action should be justified.

---

## Closed Feedback Loop

Every execution must generate observable feedback.

Every feedback signal must influence future behavior.

---

## Persistent Evolution

The system should become progressively better aligned with its objective over time.

Learning is continuous.

---

## Agent Independence

ODE Kernel should remain independent from any particular execution engine.

Examples include:

- Claude Code
- Codex
- Cursor
- Kiro
- Custom Agents

The Kernel governs them.

It does not replace them.

---

# Kernel Boundary

The Kernel owns objective continuity.

Execution engines own domain execution.

The Kernel may delegate action.

The Kernel must not delegate purpose.

This boundary is fundamental.

If no component owns objective continuity, the system may still execute but it is no longer objective-driven.

The Kernel therefore asks, before and after significant action:

> Does this action still belong to the objective?

---

# Runtime Model

The Kernel continuously maintains one runtime state.

```text
                Objective Memory
                       │
                       ▼
               Deliberation Mode
                       │
                       ▼
                  Design Mode
                       │
                       ▼
                Execution Mode
                       │
                       ▼
                 Feedback Mode
                       │
                       ▼
                Evaluation Mode
                       │
                       ▼
                  Update Mode
                       │
                       ▼
                Objective Memory
```

This cycle never terminates while the objective remains active.

---

# Runtime Modes

ODE Kernel defines six runtime modes.

---

## Objective Mode

Purpose

Understand the current objective.

Responsibilities

- load objective memory
- verify objective validity
- detect objective drift
- identify active constraints

Output

Current Objective State

---

## Deliberation Mode

Purpose

Determine the next action worth executing.

Responsibilities

- generate candidate actions
- estimate contribution
- compare alternatives
- reject low-value actions

Output

Selected Action

---

## Design Mode

Purpose

Convert decisions into executable plans.

Responsibilities

- architecture
- decomposition
- planning
- task generation

Output

Execution Plan

---

## Execution Mode

Purpose

Interact with the external world.

Examples

- coding
- searching
- calling tools
- editing files
- browsing
- generating content

Execution never modifies objectives directly.

---

## Feedback Mode

Purpose

Observe reality.

Examples

- benchmark
- tests
- runtime metrics
- screenshots
- logs
- user responses

Feedback is evidence.

Not judgment.

---

## Evaluation Mode

Purpose

Compare observed reality with desired objectives.

Responsibilities

- objective alignment
- progress estimation
- drift detection
- confidence adjustment

Output

Objective Report

---

## Update Mode

Purpose

Update persistent state.

Possible updates include:

- objective refinement
- confidence adjustment
- memory persistence
- assumption revision
- lineage extension

The update stage prepares the next iteration.

---

# Runtime State

The Kernel owns one persistent runtime state.

```yaml
kernel_state:

runtime_mode:

loop:

objective_state:

objective_memory:

current_plan:

current_execution:

feedback:

evaluation:

objective_report:
```

Every runtime transition operates on this state.

---

# Runtime Rules

The ODE Kernel enforces several invariants.

---

## Rule 1

Execution must never begin without Deliberation.

---

## Rule 2

Every execution must generate feedback.

---

## Rule 3

Every feedback must be evaluated.

---

## Rule 4

Every evaluation must update objective alignment.

---

## Rule 5

Every objective change must be persisted.

---

## Rule 6

Objectives outlive executions.

---

# Runtime Transitions

The Kernel is event-driven.

Examples

Execution Completed

↓

Feedback Mode

Feedback Complete

↓

Evaluation Mode

Objective Drift Detected

↓

Deliberation Mode

Objective Updated

↓

Objective Memory

User Changed Objective

↓

Objective Mode

Every transition is explicit.

No hidden state changes are permitted.

---

# Kernel Responsibilities

The ODE Kernel is responsible for:

- maintaining objective continuity
- coordinating runtime modes
- preserving objective memory
- initiating deliberation
- enforcing runtime rules
- detecting drift
- updating objective state
- interpreting feedback against the active objective
- preserving the relationship between objective, action, feedback, and update

The Kernel is **not** responsible for:

- writing code
- generating plans
- executing tools
- solving domain-specific problems
- owning all memory
- replacing specialized planners

Those capabilities belong to execution engines.

---

# Relationship to Previous RFCs

RFC0001 defines the philosophy.

RFC0002 defines persistent objective memory.

RFC0003 defines deliberation.

RFC0004 defines how all previous components cooperate during runtime.

It is therefore the operational specification of ODE.

---

# Future Extensions

Future RFCs may extend the Kernel with:

- Objective Evaluation
- Objective Graph
- Multi-objective Scheduling
- Value Memory
- Distributed Objective Synchronization

The Kernel should remain minimal while allowing these capabilities to evolve independently.

---

# Proposition

ODE proposes the following statement.

> **Execution engines create behavior. ODE Kernel governs behavior.**

The Kernel does not replace intelligence.

It gives intelligence continuity.

It does not replace reasoning.

It gives reasoning direction.

It does not replace execution.

It determines when execution deserves to happen.

---

# Closing Statement

An execution engine answers:

> **How can I do this?**

The ODE Kernel answers:

> **Should this be done at all, and if so, why now?**

This distinction defines the boundary between capable systems and objective-driven intelligent systems.
