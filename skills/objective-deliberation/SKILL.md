---
name: objective-deliberation
description: Deliberate on recent agent work to challenge the inferred objective, assess objective alignment, detect objective drift or proxy optimization, and choose the next objective-aligned decision. Use after meaningful coding, research, planning, refactor, testing, feature implementation, or debugging loops; before choosing the next task; when the agent seems stuck or overly focused on local details; or when the user goal is broad, ambiguous, or easy to satisfy only superficially.
---

# Objective Deliberation

Use this skill to help an agent make a better next decision. Do not simply evaluate past work. Deliberate on whether the inferred objective is right, whether the latest work moved the system closer to it, and what decision best advances the user's real outcome.

Do not replace tests, code review, or user judgment. Focus on objective progress, not implementation elegance or task completion alone.

## Inputs

Use the current conversation, artifacts, and tool results to reconstruct:

- `user_request`: What the user asked for.
- `inferred_objective`: The best current understanding of what the user actually wants to achieve.
- `current_plan`: The plan or next-step intent, if present.
- `latest_changes`: The work just completed or attempted.
- `execution_result`: Tests, logs, build results, research findings, or other evidence.
- `feedback`: User or system feedback, if present.
- `known_constraints`: Scope, timing, style, safety, or technical constraints.

If an input is missing, infer cautiously and make the uncertainty visible in `analysis` or `confidence`.

## Deliberation Workflow

Move through five phases: Understand -> Challenge -> Review -> Decide -> Coach.

1. Understand the user's real objective in outcome terms. Prefer the user's underlying success condition over the immediate task label.
2. Challenge the inferred objective. Ask: "Is this really the objective?" Consider plausible deeper objectives, narrower objectives, and missing user-success conditions.
3. Review whether the latest work improved the real objective, only a proxy, or neither.
4. Decide the next strategic move: `continue`, `pivot`, `stop`, `gather_more_information`, or `refine_objective`.
5. Coach the next agent action. Do not merely score the work; help the agent make a better next decision.

Always ask: "If we stopped now, would the user feel their objective has meaningfully progressed?"

Always end with a challenge question: "What assumption, if wrong, would most change the next decision?"

## Scoring

Use `alignment_score` from 0 to 100:

- `90-100`: Strong objective progress.
- `70-89`: Good progress with minor gaps.
- `50-69`: Partial progress.
- `30-49`: Mostly surface-task progress.
- `0-29`: Objective drift, wrong direction, or no useful progress.

Map `objective_progress` to one of: `strong`, `moderate`, `partial`, `none`, `negative`.

## Output Rules

Return a single structured report. Keep values concise and actionable. Do not add long preambles.

Use these enums exactly:

- `decision.action`: `continue`, `pivot`, `stop`, `gather_more_information`, `refine_objective`
- `objective_drift.severity`: `none`, `low`, `medium`, `high`
- `confidence`: `low`, `medium`, `high`

If context is insufficient, set `confidence: low`, explain the missing evidence, and set `decision.action: gather_more_information`.

## Output Template

```yaml
objective_deliberation_report:
  real_objective: ""
  objective_challenge:
    is_objective_certain: false
    alternative_objectives: []
    explanation: ""
  surface_task: ""
  alignment_score: 0
  objective_progress: partial
  stopped_now_answer: ""
  objective_drift:
    detected: false
    severity: none
    explanation: ""
  proxy_optimization:
    detected: false
    explanation: ""
  opportunity:
    detected: false
    description: ""
    estimated_objective_lift: ""
  analysis: ""
  decision:
    action: continue
    rationale: ""
  next_best_action: ""
  challenge: "What assumption, if wrong, would most change the next decision?"
  should_continue: true
  should_update_objective: false
  confidence: medium
```

## Calibration Examples

For "Build an AI naming website" where the latest work generates 100 names, first challenge whether the objective is naming, brand confidence, domain registration, company formation, or fast startup validation. Score around `58` if generation works but the real objective is helping users choose a commercially usable name with confidence. Flag proxy optimization if quantity of names is being optimized over confidence, availability, or fit. Prefer `decision.action: refine_objective` if the real user-success condition is unclear; prefer `continue` if the objective is clear and the next step directly increases confidence.

For "Improve checkout reliability" where the latest work refactored checkout UI components, score around `42` unless there is evidence that the refactor reduced failures. Flag objective drift if code organization displaced failure analysis, retry behavior, observability, or payment-state handling.

For "Research whether this product idea is viable" where the latest work collected competitor links, score around `64` if the links are relevant but unsynthesized. Flag proxy optimization if source count is being optimized over demand, differentiation, willingness to pay, and risk analysis.
