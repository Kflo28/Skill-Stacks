# Smoke Report Template

## Target

```text
Project/vertical:
Smoke command:
Mode:
Date/time:
Operator:
```

## Verification Commands

```text
npm run check: passed/failed/not run
npm run build: passed/failed/not run
vertical build: passed/failed/not run
smoke command: passed/failed/not run
```

## Smoke Coverage

Checked:

- [ ] app shell loaded
- [ ] navigation rendered
- [ ] primary page rendered
- [ ] list/pipeline rendered
- [ ] detail page opened
- [ ] key workflow section rendered
- [ ] action buttons visible
- [ ] no blocking console errors
- [ ] mobile viewport checked if applicable

## Failure Details

```text
Failed step:
Current URL:
Expected:
Actual:
```

## Artifacts

```text
Screenshot:
Console errors:
Failure JSON:
```

## Fix Summary

```text
Root cause:
Files changed:
Behavior after fix:
```

## Remaining Risks

```text
Subjective UI risks:
Manual auth/live-service checks still needed:
Known limitations:
```

## Final Status

```text
Smoke status: PASS / FAIL / NEEDS ATTENTION
Safe for Ryan review: YES / NO
Safe for next build: YES / NO
```