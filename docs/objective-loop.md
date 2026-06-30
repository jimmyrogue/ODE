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

Design

↓

Execution

↓

Feedback Collection

↓

Objective Evaluation

↓

Decision Filter

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

# Step 3 — Design

Generate multiple candidate approaches.

Each design should estimate:

- expected objective contribution
- implementation complexity
- execution cost
- risk

---

# Step 4 — Execution

Delegate implementation to the execution agent.

Execution may involve:

- coding
- research
- planning
- API calls
- tool usage

---

# Step 5 — Feedback Collection

Collect all observable evidence.

Never rely on success alone.

Evidence includes:

- tests
- logs
- metrics
- user behavior
- runtime data

---

# Step 6 — Objective Evaluation

Ask:

Did execution improve the objective?

Important distinction:

Task Success

≠

Objective Success

---

# Step 7 — Decision Filter

Before another iteration, evaluate all possible actions.

Decision priorities:

1. highest objective contribution
2. lowest unnecessary complexity
3. lowest long-term maintenance cost

Possible outputs:

- Continue
- Stop
- Revise
- Update Objective
- Rollback
- Ask User

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

decision:

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