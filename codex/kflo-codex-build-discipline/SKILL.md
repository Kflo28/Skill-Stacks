# K-FLO Codex Build Discipline Skill

## Purpose

Use this skill whenever Codex is modifying K-FLO code, migrations, docs, local dev scripts, or UI flows.

The purpose is to keep the build disciplined: small scopes, no accidental deploys, no fake verification, and clear reporting.

## Default Operating Rules

- Do not deploy unless Ryan explicitly says to deploy.
- Do not commit unless Ryan explicitly says to commit.
- Do not broaden scope because a nearby improvement is tempting.
- Do not fake backend/live-service success.
- Do not claim manual smoke was run if it was not run.
- Do not change insurance/default behavior while working on roofing unless explicitly requested.
- Do not change roofing while working on insurance unless explicitly requested.
- Do not weaken RLS, approval gates, or email send safety to make a test pass.

## Verification Baseline

For normal app/code changes, run:

```bash
npm run check
npm run build
VITE_KFLO_VERTICAL=roofing_exteriors npm run build
npm run dev:doctor
```

For roofing UI/workflow changes, also run:

```bash
npm run smoke:roofing
```

For JavaScript/Node script changes, also run:

```bash
node --check path/to/script.mjs
```

For Netlify function changes, run:

```bash
node --check netlify/functions/<function-name>.js
```

## Report Format

Every report should include:

```text
Changed files:
- ...

What changed:
- ...

Verification:
- npm run check: passed/failed
- npm run build: passed/failed
- roofing build: passed/failed
- npm run smoke:roofing: passed/failed if relevant

Not run:
- ...

Remaining risks:
- ...
```

If a command was not run, say why.

## Gates

Respect gates. If a prompt says do not proceed unless a polish/review pass passes, stop at the gate if it fails.

Examples:

- Do not build email sending before PDF/storage prerequisites pass.
- Do not build signatures before email approval gates pass.
- Do not build live send paths if Gmail/send transport is unavailable.

## Local Dev Command Discipline

Use the correct lane:

```bash
npm run dev:roofing
```

for local demo mode.

```bash
npm run dev:roofing:auth -- --no-open
```

for real Supabase auth without Netlify functions.

```bash
npm run dev:roofing:auth:netlify
```

for Gmail/email/API function testing through Netlify Dev.

Do not test Netlify functions from a Vite-only port.

## Database Discipline

For Supabase migrations:

- Review RLS and GRANTs separately.
- Do not add anon grants unless intentionally public.
- Service role can be broad; authenticated should be least privilege.
- Timeline/audit tables should usually be append-only: select/insert, not update/delete.
- If SQL was applied manually, document it.

## Output Philosophy

Ryan needs operator truth, not happy talk.

Say:

- what passed
- what failed
- what is untested
- what must be smoked manually
- what is safe to build next

No fog machines.
