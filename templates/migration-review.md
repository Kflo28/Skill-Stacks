# Migration Review Template

## Migration

```text
File:
Purpose:
Tables/functions/policies affected:
```

## Safety Classification

```text
Additive only: yes/no
Drops existing objects: yes/no
Alters existing columns: yes/no
Touches RLS: yes/no
Touches GRANTs: yes/no
Touches storage policies: yes/no
```

## RLS Review

```text
RLS enabled:
Anon access:
Authenticated policies:
Service role policies:
Workspace/member scoping:
Admin-only scoping:
```

## Data API Grants

```text
authenticated grants:
service_role grants:
anon grants:
append-only tables:
sequence grants:
```

## Storage Review

```text
Bucket:
Public/private:
Path convention:
Policies:
Signed URL behavior:
```

## Verification SQL

```sql
-- paste verification SQL here
```

## Apply Instructions

```text
How to apply:
Preflight checks:
Post-apply checks:
```

## Risks

```text
- risk
- risk
```

## Verdict

```text
Safe to apply: yes/no
Blocking issues:
Follow-up needed:
```