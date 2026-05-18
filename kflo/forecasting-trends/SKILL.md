# K-FLO Forecasting and Trend Skill

## Purpose

Use this skill when K-FLO needs to spot operational patterns, risks, stale work, missed follow-ups, revenue leaks, or repeated blockers.

This is not magical forecasting. V1 trend detection should be grounded in available app state and should label facts, risks, and suggested actions clearly.

## Core Rule

Do not overstate certainty.

Use:

```text
Observed fact
Inferred risk
Suggested action
```

Avoid:

```text
This will definitely happen.
```

unless the data truly proves it.

## Cross-Vertical Signals

K-FLO should look for:

- overdue follow-ups
- repeated no-response patterns
- stale opportunities
- high-value work without next action
- blocked documents
- unclosed loops
- recent activity drop-off
- tasks stuck in the same state too long
- missed customer updates
- repeated workflow failures

## Roofing Signals

For roofing, monitor:

- change orders stuck in approval_needed or work_hold
- job site checklist items open too long
- document readiness blockers
- missing production handoff
- completion photos missing
- closeout stuck open
- review request not sent
- route stops skipped repeatedly
- adjuster/claim follow-ups overdue
- high-value jobs with unresolved blockers

## Insurance Signals

For insurance, monitor:

- overdue callbacks
- no-response leads
- annual/coverage review opportunities
- clients without recent touch
- sold leads missing applications
- applications without final status
- route inefficiency
- agent activity gaps
- leads with repeated no-show/no-answer outcomes
- retention risk signals

## Output Pattern

Use a compact operations format:

```text
Signal:
- [what was detected]

Why it matters:
- [risk/opportunity]

Next move:
- [specific action]
```

For multiple signals, rank by:

1. money/revenue at risk
2. customer trust risk
3. calendar urgency
4. blocker severity
5. ease of resolution

## Forecasting Language

Use careful wording:

- “This is trending stale.”
- “This looks like a retention opportunity.”
- “This is becoming a blocker.”
- “This job may be at risk of delay.”
- “This follow-up is overdue and should be handled today.”

Avoid unsupported certainty.

## Data Sufficiency

If data is thin, say so.

Example:

```text
I only have one recent touch, so this is a weak signal. The next safe move is to follow up and log the outcome.
```

## Do Not

- Do not invent metrics.
- Do not invent trend history.
- Do not use fear language without evidence.
- Do not claim statistical forecasting when using rule-based signals.
- Do not replace human judgment for financial/legal/compliance decisions.

## Quality Check

Before giving a trend/forecast:

1. What fact triggered this?
2. Is the risk inferred or directly observed?
3. Is the next action specific?
4. Did I avoid overclaiming?
5. Did I use the correct vertical language?
