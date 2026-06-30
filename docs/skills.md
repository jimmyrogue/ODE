# ODE Skills

---

# Purpose

Skills are portable implementation artifacts for exercising parts of ODE in real agent workflows.

They are not the ODE theory itself.

They are also not a complete ODE runtime.

A skill should expose one focused piece of objective-driven control so that an existing agent can apply it consistently.

---

# Current Skills

## Objective Deliberation

Path:

```text
skills/objective-deliberation/
```

Purpose:

```text
Deliberate on recent agent work, challenge the inferred objective, assess objective alignment, detect objective drift or proxy optimization, and choose the next objective-aligned decision.
```

Use it after meaningful work loops such as:

- coding
- research
- planning
- refactoring
- testing
- feature implementation
- debugging

Use it before choosing the next significant task, especially when the agent may be stuck, overly focused on local details, or satisfying a broad user goal only superficially.

---

# Skill Contract

The functional contract lives in:

```text
skills/objective-deliberation/SKILL.md
```

This file must contain:

- YAML frontmatter with `name` and `description`
- concise Markdown instructions
- expected inputs
- deliberation workflow
- output rules
- output template

The current skill outputs an `objective_deliberation_report`.

That report should include:

- the reconstructed real objective
- objective event chain replay when available
- objective challenge
- alignment score
- objective drift assessment
- proxy optimization assessment
- next decision
- appendable objective event
- next best action

---

# OpenAI/Codex Metadata

The optional UI metadata lives in:

```text
skills/objective-deliberation/agents/openai.yaml
```

This file is not the skill logic.

It helps OpenAI/Codex surfaces display and invoke the skill with a human-facing name, short description, and default prompt.

The skill must remain understandable from `SKILL.md` alone.

---

# Invocation Example

```text
Use $objective-deliberation to review the latest work, decide whether it advanced the real objective, and choose the next objective-aligned action.
```

The skill should not merely summarize completed work.

It should answer:

> If we stopped now, would the user feel their objective has meaningfully progressed?

It should also propose the event that should be appended to the Objective Event Chain.

---

# Relationship To ODE

`objective-deliberation` maps to Deliberation Mode and post-execution objective evaluation.

It exercises these ODE responsibilities:

- reconstruct the active objective
- challenge whether the inferred objective is correct
- distinguish task completion from objective progress
- detect objective drift
- detect proxy optimization
- choose the next objective-aligned decision
- preserve a compact objective event for future memory

It does not replace:

- tests
- code review
- user judgment
- persistent Objective Memory
- the full ODE Kernel

---

# Maintenance Rules

When updating a skill:

- keep `SKILL.md` as the functional source of truth
- keep frontmatter limited to `name` and `description`
- keep triggering guidance inside `description`
- keep `agents/openai.yaml` aligned with the skill but optional
- avoid extra README or changelog files inside the skill folder
- validate the skill folder with the skill-creator validation script when available

If a skill starts carrying detailed reference material, move that material into a directly linked `references/` file instead of expanding `SKILL.md` indefinitely.
