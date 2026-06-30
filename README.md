# ODE — Objective Driven Evolution

> **ODE is a control theory for objective-driven intelligent systems.**

> **Most AI agents optimize tasks. ODE optimizes objectives.**

ODE (Objective Driven Evolution) is a control paradigm for building **objective-driven intelligence**.

It is not an agent framework, a prompt library, or a skill.

ODE defines how intelligent systems preserve objectives, deliberate before action, evaluate progress, and evolve direction over time.

Instead of asking an agent:

> *"Did you complete the task?"*

ODE continuously asks:

> *"Did you move closer to the real objective?"*

---

# Why Now?

Execution is becoming commoditized.

Planning is becoming commoditized.

Coding is becoming commoditized.

The next frontier of intelligent systems is not execution.

It is objective alignment.

ODE exists because the bottleneck has shifted from solving problems to choosing the right problems.

---

# Agent Model Comparison

```text
Traditional Agent

Task
  ↓
Plan
  ↓
Execute
  ↓
Reflect
  ↓
Done


ODE Agent

Objective
  ↓
Deliberation
  ↓
Design
  ↓
Execute
  ↓
Evaluate
  ↓
Objective Update
  ↓
Repeat
```

---

# Why ODE?

Today's AI agents are incredibly good at executing tasks.

Most modern agent frameworks follow a similar pattern:

```text
Task
    ↓
Planning
    ↓
Execution
    ↓
Reflection
    ↓
Done
```

This works well for clearly defined problems.

However, many real-world problems are **objective-driven**, not **task-driven**.

Examples:

- Building a successful product
- Designing a software architecture
- Optimizing a business
- Conducting research
- Improving user experience
- Growing a community

In these scenarios, completing individual tasks does **not necessarily** move the system closer to its real objective.

ODE introduces a missing control layer.

```text
                    Objective Memory
                           │
                           ▼
Input
   │
   ▼
Objective Discovery
   │
   ▼
Objective Formalization
   │
   ▼
────────────────────────────
        Deliberation
────────────────────────────
   │
   ▼
Design
   │
   ▼
Execution
   │
   ▼
Feedback Collection
   │
   ▼
Objective Evaluation
   │
   ▼
Objective Update
   │
   └──────────────► Objective Memory
```

The objective is continuously refined while the system evolves.

---

# Core Runtime Model

ODE is built around three core runtime components:

```text
Objective Memory
        ↓
Deliberation
        ↓
Objective Loop
```

Objective Memory preserves why the system acts.

Deliberation decides what action deserves execution.

Objective Loop executes, observes feedback, evaluates progress, and updates the objective.

Together they form the ODE control layer.

---

# Core Philosophy

Traditional agents optimize tasks.

ODE optimizes objectives.

Traditional agents ask:

- Is the task finished?
- Is the implementation correct?
- Did the tests pass?

ODE asks:

- What is the real objective?
- Does this action move closer to that objective?
- Are we optimizing a proxy instead of the real goal?
- Should the objective itself evolve?

This difference seems small.

It fundamentally changes how an autonomous agent behaves.

---

# First Principles

ODE is based on one simple observation:

> **Every intelligent system exists to optimize something.**

Software optimizes user value.

A recommendation system optimizes engagement.

A robot optimizes task completion.

A company optimizes long-term growth.

A human optimizes a constantly evolving set of personal objectives.

The implementation is only one stage.

The objective comes first.

---

# The ODE Loop

```text
Input

↓

Objective Discovery

↓

Objective Formalization

↓

Deliberation

↓

Design

↓

Execution

↓

Feedback Collection

↓

Objective Evaluation

↓

Objective Update

↓

Repeat
```

Each iteration should leave the system closer to the objective than before.

---

# Design Principles

## Objective First

Every decision should be justified by an objective.

Never implement features simply because they were requested.

Always attempt to infer the underlying user value.

---

## Objectives Can Evolve

Objectives are not fixed.

As new evidence appears, objectives may become clearer, more measurable, or even fundamentally different.

ODE treats objectives as living state.

---

## Feedback Is The Engine

Without feedback there is no evolution.

Every execution should produce measurable signals.

These signals become the basis for future decisions.

---

## Decisions Over Execution

Execution is only one capability.

Choosing the right next action is often more valuable than executing the current one faster.

---

## Optimize Contribution

The best action is not the easiest action.

The best action is the one with the highest contribution toward the objective.

---

# Architecture

```text
Objective Loop

├── Objective Discovery
├── Objective Formalization
├── Deliberation
├── Design Generator
├── Execution Runner
├── Feedback Collector
├── Objective Evaluator
└── Objective Updater
```

Each module is intentionally independent.

They may become:

- Prompt Skills
- Sub Agents
- MCP Tools
- Runtime Components

This repository already includes one experimental skill artifact:

- `skills/objective-deliberation/` - a Codex-compatible skill for post-work objective deliberation.

See `docs/skills.md` for the current skill runtime notes.

---

# Current Status

ODE is currently an experimental research project.

The first milestone focuses on defining the theory, vocabulary, and RFC foundation of objective-driven intelligence.

The project now also contains an early skill implementation of Deliberation:

- `skills/objective-deliberation/SKILL.md` defines the agent-facing workflow.
- `skills/objective-deliberation/agents/openai.yaml` defines optional OpenAI/Codex UI metadata.

This skill is not the ODE runtime.

It is a concrete, portable artifact for exercising one part of the ODE loop: evaluating recent work against the real objective and choosing the next objective-aligned decision.

The core asset remains the control theory itself.

---

# Long-term Vision

Today:

```text
Task
    ↓
Planning
    ↓
Execution
```

Tomorrow:

```text
Objective
    ↓
Deliberation
    ↓
Design
    ↓
Execution
    ↓
Feedback
    ↓
Objective Evaluation
    ↓
Objective Evolution
```

Eventually:

```text
Objective Memory

↓

Objective Graph

↓

Objective Engine

↓

Self-Evolving Agents
```

---

# Roadmap

## Phase 1

Theory

- Manifesto
- RFCs
- Core vocabulary
- Control principles

---

## Phase 2

Prompt Runtime

- Objective prompts
- Deliberation prompts
- Objective reports
- Agent-agnostic usage

---

## Phase 3

Skill Runtime

- Objective Deliberation Skill
- Objective Loop Skill
- Objective Memory Skill
- Runtime handoff patterns

---

## Phase 4

ODE Runtime

- Persistent Objective State
- Objective Memory
- Continuous Loop
- Objective Evaluation
- Objective Update

---

## Phase 5

ODE Agent

- Native objective-driven autonomous agents
- Multi-objective optimization
- Objective Graph
- Self-evolving agents

---

# Project Structure

```text
ode/

├── MANIFESTO.md

├── README.md

├── RFC/
│   ├── 0001-objective-driven-evolution.md
│   ├── 0002-Objective-Memory.md
│   ├── 0003-Deliberation.md
│   ├── 0004-ODE-Kernel.md
│   ├── 0005-ODE-Kernel-API.md
│   ├── 0006-Objective-Report.md
│   └── 0007-ODE-Protocol.md

├── docs/
│   ├── architecture.md
│   ├── ODE-architecture.md
│   ├── objective-loop.md
│   └── skills.md

├── skills/
│   └── objective-deliberation/

└── book/
```

---

# One Sentence

**Most AI agents know how to solve problems.**

**ODE teaches them how to decide which problems are worth solving—and whether they are actually getting closer to the objective.**
