---
name: objective-deliberation
description: Deliberate on recent agent work to challenge the inferred objective, assess objective alignment, detect objective drift or proxy optimization, and choose the next objective-aligned decision. Use after meaningful coding, research, planning, refactor, testing, feature implementation, or debugging loops; before choosing the next task; when the agent seems stuck or overly focused on local details; or when the user goal is broad, ambiguous, or easy to satisfy only superficially.
---

# Objective Deliberation

Use this skill to help an agent make a better next decision. Do not simply evaluate past work. Deliberate on whether the inferred objective is right, whether the latest work moved the system closer to it, and what decision best advances the user's real outcome.

This skill should treat objectives as an evolving chain, not a static variable. When available, reconstruct the current objective from the Objective Event Chain: the sequence of user requests, hypotheses, evidence, decisions, feedback, drift events, and objective refinements that explain how the current objective came to be.

Do not replace tests, code review, or user judgment. Focus on objective progress, not implementation elegance or task completion alone.

## Inputs

Use the current conversation, artifacts, and tool results to reconstruct:

- `user_request`: What the user asked for.
- `inferred_objective`: The best current understanding of what the user actually wants to achieve.
- `objective_event_chain`: The append-only chain of objective-relevant events, if available. Use it to reconstruct how the current objective emerged instead of treating the latest inferred objective as final.
- `current_plan`: The plan or next-step intent, if present.
- `latest_changes`: The work just completed or attempted.
- `execution_result`: Tests, logs, build results, research findings, or other evidence.
- `feedback`: User or system feedback, if present.
- `known_constraints`: Scope, timing, style, safety, or technical constraints.

If an input is missing, infer cautiously and make the uncertainty visible in `analysis` or `confidence`.

## Deliberation Workflow

Move through six phases: Replay -> Understand -> Challenge -> Review -> Decide -> Coach.

1. Replay the Objective Event Chain when available. Start from the latest result and trace backward through the most relevant events that explain why the current objective exists.
2. Understand the user's real objective in outcome terms. Prefer the user's underlying success condition over the immediate task label.
3. Challenge the inferred objective. Ask: "Is this really the objective?" Consider plausible deeper objectives, narrower objectives, and missing user-success conditions.
4. Review whether the latest work improved the real objective, only a proxy, or neither.
5. Decide the next strategic move: `continue`, `pivot`, `stop`, `gather_more_information`, or `refine_objective`.
6. Coach the next agent action. Do not merely score the work; help the agent make a better next decision.

Always ask: "If we stopped now, would the user feel their objective has meaningfully progressed?"

Always ask: "What event should be appended to the Objective Event Chain after this review?"

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
  objective_event_chain:
    replayed: false
    relevant_events: []
    reconstructed_objective: ""
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
  append_event:
    type: objective_review
    summary: ""
    evidence: []
    objective_delta: ""
    confidence_delta: ""
  next_best_action: ""
  challenge: "What assumption, if wrong, would most change the next decision?"
  should_continue: true
  should_update_objective: false
  confidence: medium
```

## Objective Event Chain

When available, use the Objective Event Chain as the long-term context for deliberation.

Do not treat `inferred_objective` as a fixed truth. Treat it as the current projection of an event chain.

The chain may contain events such as:

- `user_request`: A user stated or changed a request.
- `objective_hypothesis`: The agent inferred a possible real objective.
- `evidence`: New evidence changed confidence in an objective.
- `decision`: A strategic decision was made.
- `execution_result`: Work was completed or failed.
- `feedback`: User, test, runtime, market, or system feedback appeared.
- `objective_drift`: The agent drifted away from the real objective.
- `objective_refinement`: The objective was refined or reframed.

The skill should produce one `append_event` in every report. This event is the proposed next link in the chain.

The event should explain what was learned, what changed, and how the current objective should be interpreted after this deliberation.

## Calibration Examples

For "Build an AI naming website" where the latest work generates 100 names, first replay the objective event chain if available: user asked for naming, later emphasized domains, affiliate flow, and brand usefulness. Then challenge whether the objective is naming, brand confidence, domain registration, company formation, or fast startup validation. Score around `58` if generation works but the real objective is helping users choose a commercially usable name with confidence. Flag proxy optimization if quantity of names is being optimized over confidence, availability, or fit. Prefer `decision.action: refine_objective` if the real user-success condition is unclear; prefer `continue` if the objective is clear and the next step directly increases confidence.

For "Improve checkout reliability" where the latest work refactored checkout UI components, score around `42` unless there is evidence that the refactor reduced failures. Flag objective drift if code organization displaced failure analysis, retry behavior, observability, or payment-state handling.

For "Research whether this product idea is viable" where the latest work collected competitor links, score around `64` if the links are relevant but unsynthesized. Flag proxy optimization if source count is being optimized over demand, differentiation, willingness to pay, and risk analysis.

## Minimal Event Example

```yaml
objective_event_chain:
  replayed: true
  relevant_events:
    - type: user_request
      summary: "User asked to build an AI naming website."
    - type: objective_hypothesis
      summary: "Initial objective inferred as generating many names."
    - type: evidence
      summary: "User repeatedly emphasized domain availability and affiliate registration path."
    - type: objective_refinement
      summary: "Objective refined from name generation to helping users choose and register commercially usable names."
  reconstructed_objective: "Help users confidently choose and register a commercially usable brand name."

append_event:
  type: objective_review
  summary: "Latest work improved name generation but did not yet improve confidence, availability, or registration completion."
  evidence:
    - "Generated names exist."
    - "No domain availability or registration path is present yet."
  objective_delta: "Partial progress toward discovery, limited progress toward confident adoption."
  confidence_delta: "+0.05 that domain availability is a key success condition."
```
