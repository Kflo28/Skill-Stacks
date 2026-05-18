# Skill-Stacks

Reusable AI skills and operating playbooks for The Findery, K-FLO, resale research, auction scouting, and field workflow systems.

## Purpose

This repo stores reusable Agent Skills so repeatable workflows can be packaged, versioned, improved, and reused across ChatGPT, Codex, and future AI tooling.

Skills should not be memory dumps. A skill should describe a repeatable workflow, decision process, output format, and final quality check.

## Repository Structure

```text
codex/
  smoke-protocol/
  kflo-codex-build-discipline/
  supabase-rls-grants/
  netlify-dev-debug/

kflo/
  core-operator/
  roofing-context/
  insurance-context/
  forecasting-trends/
  communication-drafts/

templates/
  smoke-report.md
  build-report.md
  migration-review.md
```

## Codex Skills

Codex skills guide how the builder works. They cover verification commands, no-deploy/no-commit discipline, smoke testing, database migration review, local dev troubleshooting, and reporting standards.

Start here:

- `codex/smoke-protocol/SKILL.md`
- `codex/kflo-codex-build-discipline/SKILL.md`
- `codex/supabase-rls-grants/SKILL.md`
- `codex/netlify-dev-debug/SKILL.md`

## K-FLO Skills

K-FLO skills guide how the in-app assistant should reason. They separate the core operator brain from vertical-specific behavior.

Start here:

- `kflo/core-operator/SKILL.md`
- `kflo/roofing-context/SKILL.md`
- `kflo/insurance-context/SKILL.md`
- `kflo/forecasting-trends/SKILL.md`
- `kflo/communication-drafts/SKILL.md`

## Initial Skill Stack

- findery-listing
- kflo-review
- auction-scout
- kflo-smoke-protocol
- kflo-core-operator
- kflo-roofing-context
- kflo-insurance-context

## Default Rules

- Do not deploy unless explicitly instructed.
- Do not commit unless explicitly instructed.
- Run the relevant smoke protocol after UI/workflow changes.
- Keep vertical context explicit: Roofing is Roofing. Insurance is Insurance.
- Never auto-send customer-facing communication.
- Separate facts, inferred risks, and suggested next actions.
- Label limitations honestly instead of pretending a workflow is complete.
