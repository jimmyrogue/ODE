# RFC 0003 — Deliberation

**Status:** Draft

**Author:** ODE Contributors

**Created:** 2026

**Version:** 0.2

---

# Deliberation

## Choosing the Next Best Action

---

# Abstract

Modern AI agents are becoming extraordinarily capable at execution.

They can plan.

They can write code.

They can use tools.

They can perform long-running workflows.

Yet execution is no longer the bottleneck.

As execution becomes increasingly inexpensive, the quality of decisions becomes the dominant factor determining long-term performance.

ODE introduces **Deliberation**.

Deliberation is the process by which an intelligent system evaluates possible future actions before committing to one.

Unlike planning, which determines *how* to accomplish a task, deliberation determines *whether an action should be taken at all*, *whether it serves the current objective*, and *whether a better alternative exists*.

Deliberation may select an action.

It may also reject an action, defer action, request more evidence, or update the objective.

Execution changes the world.

Deliberation decides **which future is worth creating.**

---

# Motivation

Current agent architectures typically resemble:

```text
Task
    ↓
Planning
    ↓
Execution
    ↓
Reflection
```

Planning decides how.

Reflection evaluates what happened.

Between these two stages there is a missing capability.

Before acting, an intelligent system should ask:

- Is this the right action?
- Does it contribute to the objective?
- Is there another action with higher impact?
- Am I optimizing a proxy instead of the real objective?
- Should I act now, or continue gathering evidence?

Most agents immediately execute the first reasonable plan.

ODE argues that intelligent systems should first deliberate.

---

# Problem Statement

Execution is cheap.

Wrong decisions are expensive.

As AI systems become faster, execution cost continues to decrease.

However, the cost of choosing the wrong direction grows.

Examples include:

- building unnecessary features
- optimizing the wrong metric
- introducing architectural complexity
- collecting irrelevant information
- solving symptoms instead of causes

None of these failures arise because execution was poor.

They arise because deliberation never occurred.

---

# First Principle

> **Every action must justify its contribution to the objective before it deserves execution.**

Execution is not the default.

Execution is the consequence of successful deliberation.

An action should be treated as a commitment of attention, time, and consequence.

Deliberation exists to decide whether that commitment is justified.

---

# Deliberation as a Runtime Mode

Deliberation is not merely a function.

It is a mode of agent operation.

In Execution Mode, an agent acts.

In Reflection Mode, an agent reviews what happened.

In Deliberation Mode, an agent decides what should happen next.

ODE introduces Deliberation Mode as a required state before significant execution.

An ODE-compatible agent should enter Deliberation Mode whenever it is about to:

- create a major feature,
- change architecture,
- update an objective,
- accept a trade-off,
- introduce complexity,
- remove functionality,
- make an irreversible decision,
- or continue a loop after feedback.

The depth of deliberation should scale with consequence.

Small reversible actions may require light deliberation.

High-cost, ambiguous, irreversible, or objective-changing actions require deeper deliberation.

---

# Deliberation vs Planning

Planning answers:

> How can I accomplish this task?

Deliberation answers:

> Should this task be performed?

Planning optimizes efficiency.

Deliberation optimizes direction.

Planning assumes the objective.

Deliberation questions the objective.

Both are necessary.

Neither replaces the other.

---

# Deliberation vs Reflection

Reflection is retrospective.

It asks:

> What happened?

Deliberation is prospective.

It asks:

> What should happen next?

Reflection learns from the past.

Deliberation chooses the future.

---

# Deliberation vs Evaluation

Evaluation measures progress.

Deliberation determines action.

Evaluation produces evidence.

Deliberation consumes evidence.

These are complementary processes.

---

# The Deliberation Cycle

Every significant action should pass through the following cycle.

```text
Current Objective
        │
        ▼
Candidate Actions
        │
        ▼
Expected Contribution
        │
        ▼
Trade-off Analysis
        │
        ▼
Evidence Check
        │
        ▼
Decision
        │
        ▼
Execution
```

Execution is always the final step.

Never the first.

---

# Decision Criteria

Every candidate action should be evaluated along multiple dimensions.

Examples include:

- Objective Contribution
- Long-term Impact
- Complexity
- Risk
- Cost
- Reversibility
- Evidence Quality
- Expected Learning

No single metric should dominate every decision.

Deliberation exists precisely because real-world decisions are multi-objective.

---

# The Power to Refuse

Deliberation must be able to produce a negative decision.

An ODE-compatible system may decide:

- do not execute,
- postpone execution,
- gather more evidence,
- revise the candidate action,
- or update the objective before acting.

This refusal capability is required.

Without it, Deliberation degenerates into justification for execution.

The system must be able to say:

> This action is possible, but not aligned enough to deserve execution.

---

# Deliberation Commitment

When Deliberation selects an action, it should produce a commitment record.

The commitment record should preserve:

- selected action,
- objective served,
- evidence used,
- assumptions accepted,
- alternatives rejected,
- expected contribution,
- known risks,
- and conditions that should trigger reconsideration.

This record becomes the bridge between Deliberation and later Evaluation.

Reflection can only determine whether Deliberation was sound if the original commitment is preserved.

---

# Deliberation Is Continuous

Deliberation is not a one-time planning session.

It is an ongoing process.

Every iteration may reveal:

- new evidence
- invalid assumptions
- better alternatives
- changing constraints
- evolving objectives

Therefore deliberation must remain active throughout the entire Objective Loop.

---

# Observation

Highly capable execution without deliberation produces systems that become increasingly efficient at pursuing the wrong objective.

Increasing execution capability without improving deliberation accelerates objective drift.

For this reason, ODE considers deliberation to be a prerequisite for autonomous intelligence rather than an optional optimization.

---

# Proposition

ODE proposes the following statement.

> **Execution creates change. Deliberation chooses which change deserves to exist.**

An intelligent system should not be measured solely by how effectively it acts.

It should also be measured by how wisely it decides.

---

# Open Questions

This RFC intentionally leaves several questions open for subsequent sections.

- How should candidate actions be generated?
- How should objective contribution be estimated?
- Can deliberation itself be optimized?
- When should deliberation terminate?
- Can deliberation be interrupted?
- How should conflicting evidence be handled?
- Can multiple agents deliberate collaboratively?

These questions motivate the remainder of this RFC.
