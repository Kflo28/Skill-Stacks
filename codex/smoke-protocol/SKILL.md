# UI Smoke Protocol Skill

## Purpose

Use this skill after UI, workflow, routing, or app-state changes to verify that the app still loads, core pages render, and key user flows are not obviously broken.

This skill reduces manual smoke burden on Ryan. Codex should catch mechanical breakage before asking Ryan to review subjective product feel.

## When To Use

Use this skill after changes involving:

- page layout
- navigation
- route changes
- pipeline/list screens
- detail/project pages
- workflow buttons
- forms
- modal/sheet behavior
- local/demo state
- vertical-specific UI
- mobile layout
- Supabase-backed UI hydration
- any change likely to affect what a user sees or clicks

Do not require this skill for docs-only changes, SQL-only changes, or backend-only changes unless the backend change directly affects a visible flow.

## Core Rule

If a UI/workflow patch is made, run the project’s relevant smoke command before reporting success.

If a smoke command exists, use it.

If no smoke command exists, inspect the repo and either use the closest existing test harness or recommend creating one.

## Standard Verification Order

Run the lightest reliable checks first:

```bash
npm run check
npm run build
```

For vertical builds, also run the vertical build command when applicable:

```bash
VITE_KFLO_VERTICAL=roofing_exteriors npm run build
```

Then run the relevant smoke command:

```bash
npm run smoke:roofing
```

Use project-specific commands if different.

## K-FLO Roofing Current Smoke Command

For K-FLO Roofing local demo UI smoke:

```bash
npm run smoke:roofing
```

This smoke should use local demo/dev auto-login mode. It should not require Supabase auth, Gmail, Netlify Functions, or manual login.

Expected coverage:

- Today renders
- bottom nav shows Today, Pipeline, Route, Import, Performance
- Next Move renders
- Priority Stack renders
- Pipeline opens
- smoke/demo records render
- Rafael Price or equivalent smoke record opens
- Project Detail renders
- Change Orders render
- Project Documents render
- Document Readiness renders when expected
- Job Site Checklist renders
- Closeout renders
- Route opens
- Import opens
- Performance opens
- no blocking console errors

## Failure Protocol

If smoke fails:

1. Capture screenshot.
2. Capture console errors.
3. Record current URL.
4. Record failed step name.
5. Save artifacts to the project’s smoke artifact folder.

For K-FLO Roofing:

```text
test-results/roofing-smoke/
```

Expected artifacts:

```text
failure.png
failure.json
console-errors.json
```

Then fix only the clear failure. Do not broaden scope into new features.

## Reporting Format

Every UI/workflow report should include:

```text
Verification:
- npm run check: passed/failed
- npm run build: passed/failed
- vertical build: passed/failed if applicable
- npm run smoke:<target>: passed/failed

Smoke coverage:
- pages checked
- key flows checked

Artifacts:
- failure screenshot path if failed
- console errors path if failed

Remaining risks:
- subjective UI concerns
- manual auth/live-service checks still needed
```

## Subjective vs Mechanical Review

Codex should catch mechanical issues:

- page does not load
- button missing
- section missing
- route broken
- card clipped
- console error
- empty pipeline when smoke data should exist
- modal cannot open
- detail page cannot open

Ryan should still review subjective/product issues:

- does it feel too busy
- does a roofer understand it
- is the language right
- is the sales story right
- does the UI inspire confidence
- is the workflow useful in the real world

## Auth / Live-Service Boundaries

Basic smoke should not require:

- Supabase auth
- Gmail OAuth
- Netlify Functions
- real email sending
- real file uploads

Use separate smoke paths for those:

```bash
npm run smoke:roofing:auth
npm run smoke:roofing:netlify
```

If those are placeholders, report that honestly.

Do not fake live-service success.

## Netlify / Gmail Testing

If testing email/Gmail/Netlify Functions, use the Netlify dev command, not the Vite-only dev server.

For K-FLO Roofing email testing:

```bash
npm run dev:roofing:auth:netlify
```

Use the Netlify Dev URL, usually:

```text
http://localhost:8888/#/auth
```

Vite-only sessions should show a controlled “Email services unavailable” message rather than crashing.

## Do Not

- Do not claim smoke passed if it was not run.
- Do not ignore console errors.
- Do not rely on Ryan to find obvious broken pages.
- Do not use the flaky in-app browser pane as the only smoke method.
- Do not expand the scope when fixing smoke failures.
- Do not deploy as part of a smoke pass unless explicitly instructed.

## Goal

The goal is boring confidence.

Ryan should see the app after Codex has already confirmed the core paths work.
