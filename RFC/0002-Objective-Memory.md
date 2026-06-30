# RFC 0002 — Objective Memory

**Status:** Draft

**Author:** ODE Contributors

**Created:** 2026

**Version:** 0.2

---

# Objective Memory

## Remembering *Why* Instead of *What*

---

# Abstract

Modern AI agents primarily remember **facts**.

They remember repositories.

They remember APIs.

They remember conversations.

They remember files.

They remember tools.

In other words, today's agent memory is largely **descriptive**.

It answers questions like:

- What happened?
- What exists?
- What did the user say?
- What files were modified?

ODE proposes another kind of memory.

Instead of remembering what happened, an intelligent system should also remember **why those actions were taken**.

This RFC introduces **Objective Memory**.

Unlike traditional memory systems that preserve facts, Objective Memory preserves the evolution of objectives.

Objective Memory is not merely a storage mechanism.

It is a version control system for purpose.

It records not only what an intelligent system is optimizing, but also how and why that objective evolves over time.

It becomes the foundation of long-term objective-driven intelligence.

---

# Motivation

Consider a long-running software project.

An AI agent may remember:

```yaml
language: TypeScript

framework: React

database: PostgreSQL

last_modified_file:
  src/api/user.ts

tests:
  passed
```

All of this information is correct.

Yet none of it answers the most important question.

> **Why does this system exist?**

Suppose six months later another agent continues the project.

It understands every file.

It understands every API.

It understands every commit.

But it does **not** understand why certain architectural decisions were made.

It does **not** understand which trade-offs were accepted.

It does **not** understand what the project is ultimately optimizing.

As a result, the agent begins optimizing local improvements while slowly drifting away from the original objective.

This phenomenon is common not only in AI agents.

It also appears in software engineering, organizations, and even human decision making.

ODE argues that this happens because current memory systems preserve **facts**, but fail to preserve **objectives**.

Traditional memory systems preserve knowledge.

Objective Memory preserves direction.

Knowledge explains the past.

Direction determines the future.

An intelligent system that forgets facts may recover.

An intelligent system that forgets its objective begins optimizing the wrong future.

---

# Problem Statement

Current memory systems answer:

> What happened?

ODE asks a different question:

> Why did it happen?

These two questions are fundamentally different.

Example:

Fact Memory

```yaml
feature:
  Added domain lookup.
```

Objective Memory

```yaml
objective:
  Increase user confidence before choosing a name.

reason:
  Users hesitate because they are uncertain whether domains are available.
```

The first remembers an implementation.

The second remembers intent.

Intent survives implementation.

Implementations change.

Objectives remain.

---

# First Principle

> **Memory should preserve information that improves future objective optimization.**

Not every piece of information deserves long-term memory.

Memory is expensive.

Attention is limited.

Context windows are finite.

A future intelligent system should remember information according to one criterion:

> Will remembering this improve future decisions toward the objective?

If the answer is no, the information should eventually disappear.

---

# Fact Memory

Fact Memory describes the world.

Examples:

```yaml
repository:
  react-web

language:
  typescript

database:
  postgres

api:
  stripe
```

Fact Memory answers:

- What exists?
- What changed?
- What is currently true?

This memory is necessary.

But it is insufficient.

---

# Objective Memory

Objective Memory describes purpose.

Examples:

```yaml
objective:
  Help users discover commercially usable brand names.

why:
  Name generation alone does not create business value.

success:
  Users confidently purchase a domain.
```

Objective Memory answers:

- Why are we doing this?
- What future state are we optimizing?
- Which values influenced this decision?
- Which trade-offs were accepted?

This information is significantly more stable than implementation details.

---

# Observation

A remarkable property emerges.

Implementations evolve frequently.

Objectives evolve slowly.

Values evolve even more slowly.

This suggests that memory itself has layers.

Not every layer changes at the same speed.

This observation becomes the basis for the memory hierarchy introduced later in this RFC.

---

# Objective Memory Is Not Project Memory

It is tempting to think Objective Memory is simply another project summary.

It is not.

Project Memory answers:

> What has happened?

Objective Memory answers:

> What deserves to continue guiding future decisions?

These are fundamentally different.

One records history.

The other preserves direction.

---

# Objective Memory Is Not Context

Context is what a system can see right now.

Objective Memory is what allows the system to remain aligned across time.

Context may include:

- the current task,
- recent messages,
- open files,
- local feedback,
- or immediate constraints.

Objective Memory preserves:

- the current objective,
- the reason the objective matters,
- the lineage of objective changes,
- the evidence behind those changes,
- the assumptions currently being carried,
- and known signs of drift.

Context helps a system respond.

Objective Memory helps a system continue.

An ODE-compatible system must not treat temporary context as a substitute for Objective Memory.

---

# A Thought Experiment

Imagine two agents inherit the same repository.

Agent A receives only source code.

Agent B receives source code together with Objective Memory.

Both agents understand the code equally well.

However, Agent B also understands:

- why the architecture exists,
- why previous designs were rejected,
- which metrics matter,
- which trade-offs were intentional,
- and what future state the project is attempting to reach.

Although both agents possess identical implementation knowledge, only one possesses continuity of purpose.

ODE considers continuity of purpose to be a necessary component of long-term autonomous intelligence.

---

# Proposition

ODE proposes a stronger statement.

> **Objective Memory is to intelligence what Git is to source code.**

Git preserves how software evolves.

Objective Memory preserves how purpose evolves.

Git enables software projects to preserve implementation continuity.

Objective Memory enables intelligent systems to preserve objective continuity.

Objective Memory preserves objective continuity across time, agents, and implementations.

Both systems exist for the same reason:

To prevent the loss of history, reasoning, and continuity.

Implementations may change.

Technologies may change.

Frameworks may disappear.

Objectives should survive all of them.

Objective Memory is therefore not an enhancement to existing memory.

It is a different category of memory altogether.

---

# Open Questions

This RFC intentionally leaves several questions unanswered.

These questions will be addressed in later sections.

- How should objectives be represented?
- Can multiple objectives coexist?
- How long should objectives persist?
- How can an objective be considered obsolete?
- Can objectives conflict?
- Can objectives be inherited?
- Can objectives be revised automatically?
- How should confidence in an objective be measured?

These questions motivate the remainder of this RFC.

# Part 2 — Core Concepts

---

This section introduces the foundational concepts of Objective Memory.

These concepts intentionally avoid implementation details.

They define the language through which future ODE systems describe long-term intelligence.

---

# Objective Confidence

## Definition

Objective Confidence measures how certain an intelligent system is that its current objective accurately represents the true desired outcome.

Unlike implementation confidence, Objective Confidence is never absolute.

It evolves as new evidence appears.

---

## Motivation

A common assumption in today's agents is that user goals are fixed.

Reality is different.

Users often describe solutions instead of objectives.

Example:

User:

> Build a mobile app.

The actual objective may be:

- increase retention
- increase accessibility
- improve customer engagement

The implementation request is explicit.

The objective is inferred.

Inference always carries uncertainty.

Therefore every objective should include a confidence estimate.

---

## Example

```yaml
objective:

description:
  Help users discover memorable brand names.

confidence:
  0.61

reason:
  Inferred from conversation.

evidence:
  User repeatedly emphasized branding rather than generation.
```

As additional evidence appears, confidence should increase or decrease.

---

# Objective Lineage

## Definition

Objective Lineage records how an objective evolves over time.

Rather than storing only the latest objective, ODE preserves the complete evolutionary path.

---

## Motivation

Objectives rarely appear fully formed.

They become progressively refined.

Example:

Iteration 1

```text
Generate names.
```

Iteration 5

```text
Generate usable names.
```

Iteration 12

```text
Generate memorable names.
```

Iteration 24

```text
Help users build successful brands.
```

Notice that none of these objectives are "wrong."

Each represents a refinement of the previous understanding.

ODE treats objective evolution as a first-class artifact.

---

## Example

```yaml
objective_lineage:

- loop: 1
  objective:
    Generate names

- loop: 5
  objective:
    Generate usable names

- loop: 12
  objective:
    Generate memorable names

- loop: 24
  objective:
    Help users build memorable commercial brands
```

Objective Lineage enables future agents to understand not only the current objective, but how it emerged.

---

# Memory Horizon

## Definition

Memory Horizon describes how long a memory remains relevant for objective optimization.

Different categories of memory have different natural lifetimes.

---

## Observation

Not all knowledge should persist forever.

Examples:

Fact

```text
Current branch
```

may become obsolete tomorrow.

Objective

```text
Improve onboarding
```

may remain relevant for months.

Value

```text
Protect user privacy
```

may remain relevant indefinitely.

---

## Proposed Horizons

```text
Fact Memory

Hours → Days

Decision Memory

Days → Weeks

Feedback Memory

Weeks → Months

Objective Memory

Months → Years

Value Memory

Potentially Permanent
```

ODE therefore treats memory persistence as semantic rather than chronological.

---

# Objective Drift

## Definition

Objective Drift occurs when execution gradually optimizes something different from the intended objective.

---

## Example

Original objective

```text
Reduce screen time.
```

Current implementation

```text
Improve animation performance.
```

Animation may improve.

The objective does not.

The system has drifted.

---

## Characteristics

Objective Drift often happens gradually.

Individual decisions appear reasonable.

Collectively they move the system away from its purpose.

This makes Objective Drift difficult to detect using traditional reflection.

ODE therefore records drift explicitly.

---

# Objective Drift vs Objective Evolution

Objective change is not always drift.

ODE distinguishes two cases.

Objective Drift is change without preserved reason.

Objective Evolution is change with memory, evidence, and lineage.

```text
Objective Drift:
  The system starts optimizing a proxy without recording why.

Objective Evolution:
  The system updates the objective because feedback changed its understanding.
```

Objective Memory exists to make this distinction inspectable.

An objective may evolve.

But every meaningful objective change should preserve:

- the previous objective,
- the new objective,
- the evidence that justified the change,
- the assumptions that changed,
- and the decision that accepted the transition.

Without this preserved lineage, future systems cannot distinguish learning from drift.

---

## Example

```yaml
objective_drift:

detected:
  true

loop:
  18

reason:
  Recent iterations optimized implementation quality without measurable objective improvement.

severity:
  medium
```

---

# Objective Snapshot

## Definition

An Objective Snapshot captures the complete objective state at a particular iteration.

Unlike Fact Memory, snapshots preserve intention.

---

## Example

```yaml
objective_snapshot:

timestamp:

loop:

objective:

metrics:

constraints:

confidence:

active_assumptions:
```

Snapshots allow future agents to reconstruct historical reasoning.

---

# Objective Transition

## Definition

An Objective Transition records why one objective replaced another.

Transitions are more important than the objectives themselves.

---

## Motivation

Knowing

"What changed?"

is less useful than knowing

"Why did it change?"

---

## Example

```yaml
transition:

from:
  Generate names

to:
  Help users confidently choose names

reason:
  User hesitation was discovered to be the dominant failure point.

trigger:
  User feedback

confidence_change:
  +0.27
```

Transitions become a searchable history of learning.

---

# Objective Event

## Definition

Objective Events are significant moments that alter the understanding of the objective.

Examples include:

- discovering hidden user intent
- invalidating assumptions
- discovering better metrics
- changing constraints
- introducing new trade-offs

Objective Events form the milestones of objective evolution.

---

# Memory Evolution

Traditional memory grows through accumulation.

ODE memory grows through evolution.

The distinction is fundamental.

Traditional memory asks:

> What should be added?

ODE asks:

> What understanding has changed?

The amount of stored information is therefore less important than the quality of objective evolution.

---

# Concept Relationships

```text
                Objective
                     │
          ┌──────────┴──────────┐
          │                     │
 Objective Confidence     Objective Snapshot
          │                     │
          └──────────┬──────────┘
                     │
             Objective Lineage
                     │
          ┌──────────┴──────────┐
          │                     │
      Objective Event    Objective Transition
                     │
              Objective Drift
                     │
              Memory Evolution
```

These concepts together form the conceptual foundation of Objective Memory.

Subsequent RFCs will build upon this vocabulary.

---

# Second Principle

ODE proposes a second principle.

> **Memory should preserve the evolution of understanding rather than the accumulation of information.**

Information explains the past.

Understanding guides the future.

Objective Memory is designed to preserve the latter.

# Part 3 — Memory Model

---

Objective Memory should not be viewed as another database.

A better mental model is Git.

Git versions source code.

Objective Memory versions objectives.

Git stores commits.

Objective Memory stores transitions.

Git preserves implementation history.

Objective Memory preserves purpose evolution.

---

Previous sections introduced the philosophy of Objective Memory.

This section defines the logical data model.

The purpose of this model is not to prescribe implementation details.

Instead, it defines the minimum semantic structures required for an objective-driven intelligent system.

---

# Design Goals

Objective Memory should satisfy the following requirements.

## Persistence

Objectives should survive multiple execution loops.

Memory should not disappear simply because a task has completed.

---

## Evolution

Objectives should evolve rather than be replaced.

Every important refinement should become part of the objective history.

---

## Explainability

Every objective should be explainable.

Future agents should understand not only the objective itself, but also why it exists.

---

## Continuity

Multiple agents should be able to inherit the same Objective Memory and continue optimizing without losing direction.

---

# Memory Hierarchy

ODE proposes the following hierarchy.

```text
Value Memory
        │
        ▼
Objective Memory
        │
        ▼
Decision Memory
        │
        ▼
Feedback Memory
        │
        ▼
Fact Memory
```

Higher layers change more slowly.

Lower layers change more frequently.

Higher layers guide lower layers.

Lower layers provide evidence for higher layers.

---

# Objective State

Objective Memory is centered around a persistent Objective State.

```yaml
objective_state:

  id:

  created_at:

  updated_at:

  current_objective:

  confidence:

  status:

  lineage:

  active_constraints:

  active_metrics:

  current_assumptions:

  objective_history:

  transition_history:

  decision_history:

  feedback_summary:
```

This structure represents the complete objective state at any point in time.

---

# Current Objective

```yaml
current_objective:

  description:

  why:

  success_definition:

  confidence:

  owner:

  priority:
```

The current objective is always considered the best current understanding.

It is never assumed to be perfect.

---

# Objective History

Instead of overwriting objectives, ODE preserves every meaningful revision.

```yaml
objective_history:

- version:

  description:

  confidence:

  discovered_at:

  replaced_at:

  reason:
```

This enables reconstruction of objective evolution.

---

# Transition History

Every objective change should create an explicit transition.

```yaml
transition:

  id:

  from:

  to:

  trigger:

  reason:

  evidence:

  confidence_delta:
```

Transitions explain learning.

Objectives alone do not.

---

# Assumptions

Objectives often depend on assumptions.

Those assumptions should be explicitly stored.

```yaml
assumptions:

- description:

  confidence:

  supporting_evidence:

  invalidation_conditions:
```

Example

```yaml
description:

Users care more about domain availability than logo quality.

confidence:

0.72
```

If this assumption becomes invalid, objective re-evaluation should occur.

---

# Constraints

Objectives never exist in isolation.

They are constrained.

```yaml
constraints:

- budget

- latency

- regulations

- privacy

- platform

- deadline
```

Constraints influence design without changing the objective itself.

---

# Metrics

Objectives should define measurable signals.

```yaml
metrics:

- name:

  direction:

  current_value:

  target:

  confidence:
```

Metrics are not objectives.

Metrics are evidence.

Confusing the two often leads to optimization of proxy measurements.

---

# Objective Events

Every important learning event becomes part of memory.

```yaml
objective_event:

  type:

  timestamp:

  description:

  evidence:

  impact:
```

Possible event types include

- ObjectiveCreated

- ObjectiveRefined

- ObjectiveMerged

- ObjectiveSplit

- ObjectiveDeprecated

- ObjectiveConflictDetected

- ObjectiveConfidenceChanged

These events form the evolutionary history of the objective.

---

# Decision Memory

Objective Memory also stores decisions that significantly influenced objective optimization.

```yaml
decision:

  action:

  alternatives:

  selected:

  rejected:

  reason:

  expected_contribution:

  observed_result:
```

Future agents should avoid repeatedly evaluating already-understood trade-offs.

---

# Feedback Summary

Raw feedback should remain in Feedback Memory.

Objective Memory stores only summarized conclusions.

```yaml
feedback_summary:

positive_patterns:

negative_patterns:

unresolved_questions:

confidence:
```

This prevents Objective Memory from becoming overloaded with implementation details.

---

# Objective Snapshot

Every iteration produces a snapshot.

```yaml
objective_snapshot:

loop:

timestamp:

objective:

confidence:

metrics:

assumptions:

constraints:

alignment_score:

decision:
```

Snapshots allow replay of objective evolution.

---

# Objective Lineage Graph

Although Objective Lineage was previously described conceptually, the logical model treats it as a directed graph.

```text
Generate Names
        │
        ▼
Generate Usable Names
        │
        ▼
Generate Memorable Names
        │
        ▼
Build Strong Brands
```

Each node represents an objective.

Each edge represents a transition supported by evidence.

This allows future agents to reason about objective evolution instead of observing only the latest state.

---

# Memory Lifecycle

Objective Memory evolves through four stages.

```text
Discover

↓

Validate

↓

Persist

↓

Refine
```

Objectives should never jump directly into long-term memory.

Only validated objectives become persistent.

---

# Third Principle

> **Objectives should be versioned, not overwritten.**

Versioning is not about preserving history for its own sake.

It is about preserving the reasoning that produced the present.

Without versioning, intelligence loses continuity.

Without continuity, optimization becomes directionless.

Every objective is a hypothesis.

Every revision is evidence.

Together they form the evolutionary history of intelligence.

---

# Discussion

Traditional memory systems accumulate information.

ODE accumulates understanding.

Traditional memory asks:

> What do I know?

Objective Memory asks:

> Why do I believe this objective is worth pursuing?

This distinction transforms memory from passive storage into an active component of intelligent decision making.

---

# Drawbacks

Objective Memory introduces additional state management complexity.

Long-lived objective histories may become difficult to maintain.

Objective evolution may occasionally preserve incorrect assumptions.

---

# Alternatives

- Traditional Fact Memory
- Task History
- Conversation Summaries
- Knowledge Graphs

These systems preserve knowledge.

ODE preserves purpose.

---

# Unresolved Questions

- Should Objective Memory be editable?
- Can multiple agents own the same objective?
- Can objectives merge?
- Can objectives fork?
- Should objectives expire automatically?
- How should conflicting objectives be resolved?

---

# Relationship to Deliberation

Objective Memory provides the historical context required for Deliberation.

Without Objective Memory, Deliberation can only reason from the current prompt.

With Objective Memory, Deliberation can reason across time.

It can ask:

- Why was this objective created?
- How has it evolved?
- Which previous decisions were rejected?
- Which assumptions were invalidated?
- What objective drift has already occurred?

Objective Memory gives Deliberation continuity.

Deliberation gives Objective Memory agency.

---

# Closing Statement

Objective Memory is not simply memory with better summaries.

It is version control for purpose.

Just as Git enables software projects to preserve implementation history, Objective Memory enables intelligent systems to preserve objective history.

A system that can remember how its objectives evolved can continue learning without losing its direction.
