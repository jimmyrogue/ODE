# Objective Loop

---

# Purpose

The Objective Loop is the control cycle of ODE.

It continuously aligns action with the current objective, interprets feedback, and updates objective memory.

The loop is not complete when execution ends.

The loop is complete only after feedback has been evaluated, an Objective Report has been produced, and Objective Memory has been updated.

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
Decision / Commitment
↓
Design
↓
Execution
↓
Feedback Collection
↓
Objective Evaluation
↓
Objective Report
↓
Objective Memory Update
↓
Next Loop
```

---

# Step 1 — Objective Discovery

Question:

> What is the user actually trying to achieve?

Do not assume the literal task is the objective.

Infer the underlying value, desired future state, and anti-goals.

---

# Step 2 — Objective Formalization

Transform the discovered objective into an evaluable objective state.

The objective state may include:

- primary objective
- secondary objectives
- success signals
- proxy metrics
- constraints
- assumptions
- tradeoffs

The objective does not need to be mathematical.

It must be explicit enough to evaluate future action.

---

# Step 3 — Deliberation

Evaluate candidate actions before design and execution.

Deliberation asks:

- Should this action be performed at all?
- Does it contribute to the objective?
- Is there another action with higher impact?
- What tradeoffs does this action introduce?
- Is the available evidence strong enough?
- Should the system refuse, defer, or gather more evidence?
- Should the objective itself be updated before acting?

Deliberation may produce:

- execute
- refuse
- defer
- gather more evidence
- revise action
- update objective
- ask user

Execution is not the default.

Execution is the result of successful deliberation.

---

# Step 4 — Decision / Commitment

When Deliberation selects an action, it should preserve a commitment record.

The commitment record should include:

- selected action
- objective served
- expected contribution
- evidence used
- assumptions accepted
- alternatives rejected
- known risks
- reconsideration conditions

This record allows later evaluation to inspect whether the action was justified.

---

# Step 5 — Design

Convert the selected action into an executable plan.

Design should preserve the objective rationale.

Each design should estimate:

- expected objective contribution
- implementation complexity
- execution cost
- risk
- validation method

---

# Step 6 — Execution

Delegate implementation to the execution engine.

Execution may involve:

- coding
- research
- planning
- external system interaction
- tool usage
- file changes

Execution produces artifacts and observable change.

Execution does not directly update the objective.

---

# Step 7 — Feedback Collection

Collect observable evidence.

Never rely on success alone.

Evidence includes:

- tests
- logs
- metrics
- user behavior
- runtime data
- external feedback
- manual review

Feedback is evidence.

It becomes judgment only after evaluation.

---

# Step 8 — Objective Evaluation

Ask:

> Did execution improve the objective?

Important distinction:

```text
Task Success
≠
Objective Progress
```

Evaluation should distinguish:

- surface task completion
- local success
- objective progress
- objective drift
- learning from failure
- confidence change

---

# Step 9 — Objective Report

Every completed loop must produce an Objective Report.

An Objective Report should include:

```yaml
objective_report:
  metadata:
  objective:
  execution:
  decision:
  evaluation:
  objective_update:
  next_iteration:
```

The report should answer:

- What objective was active?
- What action was chosen?
- Why was it chosen?
- What happened?
- Did the task succeed?
- Did the objective progress?
- Did drift occur?
- What should happen next?

---

# Step 10 — Objective Memory Update

Update Objective Memory after the report is produced.

Memory should preserve:

- current objective
- objective lineage
- transition history
- decision history
- feedback summary
- drift events
- rejected alternatives

Objective change must preserve evidence and reason.

Without lineage, future systems cannot distinguish evolution from drift.

---

# Controller Questions

Before each significant action, the controller should ask:

> What is the active objective?

> What task is being proposed?

> Does the task serve the objective?

> What evidence supports this action?

> What assumptions are being accepted?

> What should be refused or deferred?

> What would count as objective progress?

> What would count as objective drift?

> What must be remembered for the next loop?

These questions describe controller responsibilities.

They are not an input template.

---

# Success Criteria

An Objective Loop is healthy when:

- actions remain downstream of objectives,
- significant actions pass through deliberation,
- non-execution decisions are allowed,
- feedback is interpreted against the objective,
- task success is distinguished from objective progress,
- objective drift is detected early,
- objective changes preserve lineage,
- and every loop produces an Objective Report.
