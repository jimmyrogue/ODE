# Objective Loop

---

# Purpose

Objective Loop is the runtime control algorithm of ODE.

It continuously aligns execution with the current objective.

---

# Loop

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

Loop
```

---

# Step 1 — Objective Discovery

Question:

> What is the user actually trying to achieve?

Do not accept the literal request immediately.

Infer the underlying value.

---

# Step 2 — Objective Formalization

Transform abstract goals into measurable objectives.

Example:

Instead of:

> Better UX

Produce:

- shorter completion time
- fewer failed actions
- higher retention

---

# Step 3 — Deliberation

Evaluate candidate actions before design and execution.

Deliberation asks:

- Should this action be performed at all?
- Does it contribute to the objective?
- Is there another action with higher impact?
- What trade-offs does this action introduce?
- Is the available evidence strong enough?

Decision Filter is an internal part of Deliberation, responsible for choosing among candidate actions.

---

# Step 4 — Design

Generate multiple candidate approaches.

Each design should estimate:

- expected objective contribution
- implementation complexity
- execution cost
- risk

---

# Step 5 — Execution

Delegate implementation to the execution agent.

Execution may involve:

- coding
- research
- planning
- API calls
- tool usage

---

# Step 6 — Feedback Collection

Collect all observable evidence.

Never rely on success alone.

Evidence includes:

- tests
- logs
- metrics
- user behavior
- runtime data

---

# Step 7 — Objective Evaluation

Ask:

Did execution improve the objective?

Important distinction:

Task Success

≠

Objective Success

---

# Step 8 — Objective Update

Objectives should change only when supported by evidence.

Typical reasons:

- assumptions invalid
- wrong proxy metric
- better objective discovered
- user values changed

---

# Objective Report

Every iteration must produce:

```yaml
objective_report:

real_objective:

current_action:

alignment_score:

objective_progress:

surface_task_completed:

objective_drift:

feedback_summary:

deliberation_decision:

next_action:

should_continue:

should_update_objective:
```

The next iteration must consume this report before planning again.

---

# Core Prompt

Before every iteration, the controller asks:

> What is the real objective?

> Did the last action move closer to that objective?

> Am I optimizing a proxy instead of the real objective?

> What action deserves execution?

> Should I do this at all?

> Is there a higher-impact action available?

> Should the objective itself evolve?

Only after answering these questions may the next iteration begin.

---

# Success Criteria

An Objective Loop is successful when:

- every iteration increases objective alignment,
- objective drift is detected early,
- unnecessary work is avoided,
- and the agent continuously converges toward the real objective rather than merely completing tasks.
