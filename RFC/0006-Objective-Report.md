# RFC 0006 — Objective Report

**Status:** Draft

**Author:** ODE Contributors

**Created:** 2026

**Version:** 0.1

---

# Objective Report

## The Standard Output of Objective-Driven Intelligence

---

# Abstract

Previous RFCs defined how an objective-driven intelligent system stores objectives, deliberates, executes, and evolves.

This RFC defines the standard output of one Objective Loop.

Every completed loop should produce one **Objective Report**.

Execution engines produce artifacts.

ODE produces Objective Reports.

An Objective Report is the canonical representation of what an intelligent system currently believes, why it believes it, what changed during the latest iteration, and what should happen next.

---

# Motivation

Traditional execution engines typically end with one of the following outputs:

- Success
- Failure
- Logs
- Test Results
- Generated Code

These outputs describe execution.

They do not describe understanding.

They rarely answer:

- Did the objective become clearer?
- Did the system move closer to the objective?
- What assumptions changed?
- What evidence was collected?
- What should happen next?

ODE introduces Objective Reports to answer these questions.

---

# First Principle

> **Every Objective Loop should leave behind an explanation, not merely an artifact.**

Artifacts describe what changed.

Objective Reports describe why the system changed.

---

# Design Goals

An Objective Report should satisfy the following goals.

## Explainability

A future agent should understand why the previous loop made its decisions.

---

## Continuity

The report should provide enough information to continue optimization without rethinking the entire problem.

---

## Auditability

Every major decision should be traceable.

---

## Machine Readability

Reports should have a stable schema suitable for automated processing.

---

## Human Readability

Reports should remain understandable without reading implementation details.

---

# Report Structure

Every Objective Report consists of five logical sections.

```text
Metadata

↓

Objective State

↓

Execution Summary

↓

Evaluation

↓

Next Iteration
```

---

# Metadata

Metadata identifies the report.

Example

```yaml
metadata:

  report_id:

  kernel_version:

  loop:

  timestamp:

  runtime:

  execution_engine:
```

Metadata is descriptive.

It contains no reasoning.

---

# Objective State

The report records the objective after the current iteration.

```yaml
objective:

  description:

  confidence:

  objective_alignment:

  objective_progress:

  drift_detected:

  assumptions:

  constraints:
```

This section represents the current understanding of the objective.

---

# Execution Summary

Execution describes observable actions.

```yaml
execution:

  selected_action:

  completed_actions:

  artifacts:

  external_tools:

  execution_result:
```

Execution should remain implementation-agnostic.

---

# Evaluation

Evaluation compares the observed outcome with the intended objective.

```yaml
evaluation:

  objective_contribution:

  positive_observations:

  negative_observations:

  newly_discovered_constraints:

  evidence:

  confidence_delta:
```

Evaluation measures learning rather than completion.

---

# Decision Summary

The report records why the chosen action was selected.

```yaml
decision:

  selected_action:

  alternatives:

  rejected_actions:

  reasoning:

  expected_contribution:
```

This preserves deliberation history.

---

# Objective Evolution

Objective Reports explicitly record objective evolution.

```yaml
objective_update:

  previous_objective:

  current_objective:

  updated:

  update_reason:
```

If no update occurred:

```yaml
updated: false
```

Explicitly recording the absence of change is as important as recording change itself.

---

# Next Iteration

The report concludes by recommending the next objective-driven action.

```yaml
next_iteration:

  recommended_action:

  priority:

  required_information:

  should_continue:

  should_pause:

  requires_user_input:
```

Every Objective Report points toward the next loop.

---

# Complete Example

```yaml
objective_report:

  metadata:

    loop: 18

    runtime: ODE Kernel

  objective:

    description: Improve onboarding completion

    confidence: 0.84

    objective_alignment: 81

    objective_progress: "+14%"

    drift_detected: false

  execution:

    selected_action:

      Reduce registration friction

    completed_actions:

      - Simplified signup form

      - Removed unnecessary validation

  evaluation:

    objective_contribution:

      High

    confidence_delta:

      +0.05

  decision:

    reasoning:

      Registration abandonment remained the dominant bottleneck.

  objective_update:

    updated: false

  next_iteration:

    recommended_action:

      Improve first-session activation

    should_continue: true
```

---

# JSON Schema

Every Objective Report should be serializable.

A compliant implementation should expose an equivalent JSON representation.

```json
{
  "metadata": {},
  "objective": {},
  "execution": {},
  "evaluation": {},
  "decision": {},
  "objective_update": {},
  "next_iteration": {}
}
```

Implementations may extend the schema.

They should not remove required semantic fields.

---

# Persistence

Objective Reports are immutable.

Once generated, they should never be modified.

Corrections should be represented by generating a new report.

Reports form an append-only history.

---

# Objective Timeline

An Objective Timeline is an ordered collection of Objective Reports.

```text
Report 1

↓

Report 2

↓

Report 3

↓

Report 4
```

Objective Memory may reconstruct its state from an Objective Timeline.

Future RFCs define timeline semantics in greater detail.

---

# Relationship to Previous RFCs

RFC0002 introduced Objective Memory.

RFC0006 defines the unit from which Objective Memory is built.

RFC0003 introduced Deliberation.

RFC0006 records the result of Deliberation.

RFC0004 introduced the ODE Kernel.

RFC0006 defines the standard output produced by one Kernel iteration.

RFC0005 defined the Kernel API.

RFC0006 specifies the output generated by that API.

---

# Compatibility

An implementation is ODE-compatible if every completed Objective Loop produces an Objective Report that preserves the semantic structure defined by this RFC.

The internal implementation is irrelevant.

The report is the contract.

---

# Proposition

ODE proposes the following statement.

> **Execution engines produce artifacts. ODE produces Objective Reports.**

Artifacts represent completed work.

Objective Reports represent accumulated understanding.

Understanding—not artifacts—is the true product of an objective-driven intelligent system.

---

# Closing Statement

Traditional software records what changed.

ODE records why change happened.

Every Objective Report becomes one permanent step in the evolution of intelligence.

Over time, these reports form something larger than execution history.

They become the evolutionary history of purpose itself.