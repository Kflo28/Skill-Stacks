---
name: kflo-review
description: Review K-FLO code, workflows, UI, screenshots, patches, field-operator logic, and roadmap decisions using Ryan's Supabase-first, approval-gated, conservative-write doctrine.
---

# K-FLO Review Skill

Use this skill when reviewing, designing, debugging, or improving K-FLO, Lead Sentinel, roofing/exteriors workflows, insurance workflows, field-agent workflows, admin screens, bridge behavior, inbox intake, Supabase data flow, Google Sheets mirror flow, or local app code.

## Core Identity

K-FLO is an operator-first field execution system. It is not a generic CRM. It exists to help real people move work through the field with fewer missed steps, clearer next actions, safer data flow, and stronger operator control.

## Current Architecture Truth

K-FLO has moved to a Supabase-first architecture.

Preserve this truth unless Ryan explicitly commands otherwise:

- Supabase tables are the source of truth.
- Google Sheets is now a mirrored viewing/reporting layer for Ryan, not the primary system of record.
- The app should read/write through the approved Supabase data path.
- Sheets sync/mirror behavior must not overwrite or corrupt Supabase truth.
- Any Sheets-facing lane is downstream unless explicitly designed as a controlled import.
- Approval gates still matter before risky writes, promotions, deletes, merges, or state transitions.
- Staged/previewed data should be promoted into Supabase only after approval.

## Core Doctrine

Preserve these invariants unless Ryan explicitly commands otherwise:

- Supabase is the system of record.
- Tables and relationships must remain coherent.
- Mirror-to-Sheets is for visibility, auditing, and Ryan-friendly review.
- Writes remain approval-gated until proven safe.
- Detection should be aggressive.
- Writes should be conservative.
- Preview before promotion.
- Stage before commit.
- Operator approval before risky action.
- No scope widening without explicit approval.
- No transport changes without explicit approval.
- No silent data mutation.
- No treating demo fallback data as live truth.
- No introducing a second source of truth.

## Review Priorities

When reviewing K-FLO work, evaluate in this order:

1. Does this preserve Supabase as the source of truth?
2. Does this avoid creating a competing Sheets truth layer?
3. Does this match the real field workflow?
4. Does this keep the operator moving?
5. Does this reduce clicks, confusion, or double entry?
6. Does this keep risky writes behind approval?
7. Does this stage or preview uncertain data before committing?
8. Does this work on mobile field screens?
9. Does this provide a clear next best action?
10. Does this avoid generic CRM behavior?
11. Does this keep K-FLO productizable across verticals?

## Field Workflow Lens

Always ask:

- Who is holding the phone or laptop?
- Where are they physically standing?
- What decision are they trying to make?
- What is the next action they need?
- What would slow them down?
- What would cause bad data?
- What needs approval before it becomes permanent?
- Which Supabase table/state does this action affect?
- Does any Sheets mirror update need to happen after the Supabase change?

## Data Flow Lens

When reviewing data behavior, identify:

- Source table or tables.
- Write path.
- Read path.
- Approval gate.
- Sync or mirror path to Sheets, if any.
- Failure mode if Supabase succeeds but Sheets mirror fails.
- Failure mode if a stale Sheet row exists.
- Whether the UI is showing live data, staged data, demo data, or mirrored data.

## Code Review Behavior

Prefer:

- Smallest safe patch.
- Clear file-level summary.
- No architecture wandering.
- No unnecessary abstractions.
- No broad refactors unless Ryan asks.
- No data model expansion unless justified.
- Tests before confidence.
- Honest remaining risks.

## Verification Expectations

Recommend or run the lightest sufficient checks for the change type:

- npm run check
- npm run build
- npm run smoke:roofing
- VITE_KFLO_VERTICAL=roofing_exteriors npm run build
- npm run dev:doctor
- Supabase read/write path test when data behavior changes
- Sheets mirror verification when mirror behavior changes

Do not claim verification passed unless it actually ran and passed.

## Output Format

Use this format when reviewing K-FLO changes:

1. Verdict
2. What looks right
3. What is risky
4. Smallest safe patch
5. Test commands
6. Remaining risks
7. Next best move

## Roadmap Lens

When discussing K-FLO strategy, keep these product modes in mind:

- Field Mode for reps, field agents, canvassers, inspectors, and route work.
- Advisor Mode for relationship and portfolio agents.
- Manager Mode for owners and managers.
- Hermes Operator Console as a separate conversation-first command deck, not basic admin.

## Roofing / Exteriors Focus

For roofing and exteriors, evaluate whether the system supports:

- lead intake
- canvassing routes
- inspection routes
- estimate follow-up
- adjuster meetings
- change orders
- project documents
- job site checklist
- production handoff
- closeout
- mobile-first field use

## Email / Intake Focus

For lead intake, preserve this lane:

- Pull or receive source message.
- Preserve raw source.
- Classify lead vs non-lead.
- Extract useful fields.
- Stage a preview.
- Require approval before promotion.
- Promote approved records into Supabase.
- Mirror approved data to Sheets only if the mirror lane is part of that workflow.
- Avoid broad inbox access unless explicitly requested.

## Hard Rules

- Do not remove approval gates unless Ryan explicitly commands it.
- Do not broaden Gmail, Sheets, inbox, Supabase, or external account access unless explicitly commanded.
- Do not change the transport layer unless explicitly commanded.
- Do not write to Sheets as if it is the source of truth.
- Do not let Sheets mirror logic overwrite Supabase truth.
- Do not hide uncertainty.
- Do not confuse demo fallback previews with live production data.
- Do not optimize the UI in a way that breaks the field workflow.

## Final Quality Check

Before final answer, confirm:

- Supabase source-of-truth model is preserved.
- Sheets is treated as mirror/viewing layer unless Ryan says otherwise.
- Approval gates are preserved.
- Field workflow is respected.
- Mobile risk is considered.
- Test path is named.
- Remaining risk is stated.
- Next move is concrete.
