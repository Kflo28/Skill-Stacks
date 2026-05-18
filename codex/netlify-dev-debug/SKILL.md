# Netlify Dev Debug Skill

## Purpose

Use this skill when local Netlify Dev, Vite, Gmail functions, or `/api/*` routes fail during K-FLO development.

The goal is to separate frontend-only testing from full Netlify function testing and avoid chasing the wrong port.

## Core Rule

Vite-only servers are not enough for Gmail/API function tests.

Use the correct lane:

```bash
npm run dev:roofing
```

Local demo UI only.

```bash
npm run dev:roofing:auth -- --no-open
```

Real Supabase auth without Netlify functions.

```bash
npm run dev:roofing:auth:netlify
```

Real Supabase auth plus Netlify Functions for Gmail/email/API testing.

## Ports

Common local ports:

```text
5173/5174/5175 = Vite frontend targets
8888 = Netlify Dev URL with functions
```

For email/Gmail tests, use:

```text
http://localhost:8888/#/auth
```

Do not test Gmail send/status from a Vite-only port.

## Common Failure: fetch failed

If a frontend-only Vite session calls `/api/*`, Vite may proxy to `127.0.0.1:8888`. If Netlify Dev is not running, calls fail.

Expected controlled behavior:

```text
Email services are not available in this local frontend-only session. Start Netlify Dev to test Gmail send/reply features.
```

Do not let this become a red Vite overlay.

## Common Failure: White Screen on Netlify Dev

If Netlify Dev loads functions but the browser is white and console says module MIME errors for:

- `/@vite/client`
- `/@react-refresh`
- `/src/main.tsx`

then Netlify Dev is serving or rewriting Vite module paths incorrectly.

Fix direction:

- ensure Netlify Dev proxies to the Vite target port
- ensure Vite dev module URLs resolve from the Vite origin if needed
- keep `/api/*` routed to Netlify Functions
- do not rewrite Vite module paths to `/index.html`

## Port Collision Check

If Netlify Dev cannot acquire port 8888:

Windows PowerShell:

```powershell
netstat -ano | findstr :8888
```

Kill the PID if safe:

```powershell
taskkill /PID <PID> /F
```

Or use a launcher that supports fallback ports.

## Gmail Function Checks

When Netlify Dev is running, verify:

```text
/api/gmail-oauth-status
/api/gmail-send-message
/api/gmail-reply-monitor
```

Functions should return controlled authenticated errors when unauthenticated, not proxy failures.

## Verification

After local dev script changes, run:

```bash
node --check scripts/start-roofing-netlify.mjs
npm run check
npm run build
VITE_KFLO_VERTICAL=roofing_exteriors npm run build
npm run dev:doctor
```

Then start:

```bash
npm run dev:roofing:auth:netlify
```

Check:

- auth page loads at Netlify Dev URL
- no Vite module MIME errors
- `/api/gmail-oauth-status` reaches Netlify Functions
- Vite-only sessions still show controlled email-unavailable copy

## Do Not

- Do not use Vite-only URLs for Gmail send smoke.
- Do not assume Netlify Dev is running just because a browser page opened.
- Do not ignore port collision messages.
- Do not deploy to fix a local dev script issue.

## Report Format

```text
Root cause:
- ...

Correct URL:
- ...

Changed files:
- ...

Verification:
- ...

Remaining risks:
- ...
```
