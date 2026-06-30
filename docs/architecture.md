# ODE Architecture

This document is the short architecture index for ODE.

For the conceptual explanation, read the Book.

For normative semantics, read the RFCs.

This document summarizes how the major parts fit together.

---

# Core Idea

ODE introduces an **Objective Layer** above planning and execution.

The Objective Layer preserves one invariant:

> Action must remain accountable to an evolving objective.

The system may delegate execution.

It must not delegate objective continuity.

---

# Control Stack

```text
Objective Layer
      ↓
ODE Kernel
      ↓
Deliberation
      ↓
Design
      ↓
Execution Engine
      ↓
Feedback
      ↓
Evaluation
      ↓
Objective Memory
      ↓
Objective Report
```

The ODE Kernel is the minimal control core.

It is not the execution engine.

It coordinates objective state, deliberation, feedback, evaluation, objective updates, and reports.

The current repository includes one concrete skill artifact, `skills/objective-deliberation/`, that exercises Deliberation Mode in an existing agent environment.

That skill is an implementation artifact, not the Kernel itself.

---

# Runtime Modes

ODE-compatible systems operate through these modes.

## Objective Mode

Discover, load, and formalize the current objective.

## Deliberation Mode

Evaluate candidate actions before execution.

Deliberation may choose, refuse, defer, request more evidence, or update the objective.

## Design Mode

Convert an accepted decision into an executable plan.

## Execution Mode

Delegate action to the underlying execution engine.

Execution must not silently modify objectives.

## Feedback Mode

Collect observable evidence.

Feedback is evidence, not judgment.

## Evaluation Mode

Compare observed reality against the active objective.

Distinguish task success from objective progress.

## Update Mode

Persist objective memory, objective reports, and justified objective changes.

---

# Required Invariants

An ODE-compatible system should preserve these invariants.

- Execution must not begin before deliberation.
- Every significant action must be justified against the active objective.
- Deliberation must be able to produce non-execution decisions.
- Feedback must be evaluated against the objective.
- Objective changes must preserve lineage and evidence.
- Objective Reports must close each loop.
- Objective Memory must preserve direction, not just context.

---

# Implementation Artifacts

ODE concepts may appear as prompts, skills, subagents, MCP tools, runtime components, or native agents.

The current implementation artifact is documented in `docs/skills.md`.

Its boundary is important:

- `SKILL.md` defines the portable agent-facing workflow.
- `agents/openai.yaml` defines optional OpenAI/Codex UI metadata.
- The skill can guide a single deliberation step.
- The skill does not provide persistent Objective Memory or a full ODE Kernel.
