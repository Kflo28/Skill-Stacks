# Supabase RLS and Data API Grants Skill

## Purpose

Use this skill when creating, reviewing, or applying Supabase migrations for K-FLO or related projects.

The goal is to keep database access secure, explicit, and durable across Supabase Data API behavior changes.

## Core Concepts

GRANTs and RLS are different layers.

```text
GRANT = can this role touch the table at all?
RLS = which rows can this role touch?
```

Both are required.

Do not assume RLS alone is enough. Do not assume GRANT alone is safe.

## Default Role Rules

### anon

Do not grant anon access unless the table/view is intentionally public.

For K-FLO workflow tables, anon should normally have no access.

### authenticated

Grant only the operations the app needs.

Typical patterns:

```sql
grant select, insert, update on public.some_workflow_table to authenticated;
```

Append-only audit tables usually get:

```sql
grant select, insert on public.some_audit_table to authenticated;
```

Avoid authenticated grants for:

- truncate
- trigger
- references
- delete unless the app truly needs it

### service_role

Service role may have broad access for server-side functions and admin workflows.

```sql
grant all privileges on public.some_table to service_role;
```

Never expose service-role keys in frontend code.

## Roofing Table Grant Pattern

For K-FLO Roofing:

```sql
revoke all privileges
on public.roofing_route_stop_statuses,
   public.roofing_change_orders,
   public.roofing_job_site_checklist_items,
   public.roofing_documents,
   public.roofing_timeline_events
from authenticated;

grant select, insert, update on public.roofing_route_stop_statuses to authenticated;
grant select, insert, update on public.roofing_change_orders to authenticated;
grant select, insert, update on public.roofing_job_site_checklist_items to authenticated;
grant select, insert, update on public.roofing_documents to authenticated;
grant select, insert on public.roofing_timeline_events to authenticated;

grant all privileges
on public.roofing_route_stop_statuses,
   public.roofing_change_orders,
   public.roofing_job_site_checklist_items,
   public.roofing_documents,
   public.roofing_timeline_events
 to service_role;
```

## Verification Query

Use focused checks instead of broad noisy ones:

```sql
select grantee, table_name, privilege_type
from information_schema.role_table_grants
where table_schema = 'public'
  and table_name in (
    'roofing_route_stop_statuses',
    'roofing_change_orders',
    'roofing_job_site_checklist_items',
    'roofing_documents',
    'roofing_timeline_events'
  )
  and grantee = 'authenticated'
order by table_name, privilege_type;
```

Expected:

```text
roofing_change_orders: INSERT, SELECT, UPDATE
roofing_documents: INSERT, SELECT, UPDATE
roofing_job_site_checklist_items: INSERT, SELECT, UPDATE
roofing_route_stop_statuses: INSERT, SELECT, UPDATE
roofing_timeline_events: INSERT, SELECT
```

## Migration Safety

When adding broad grant migrations across app tables, use existence checks if production may not have every optional table yet.

Pattern:

```sql
do $$
begin
  if to_regclass('public.some_table') is not null then
    grant select, insert, update on table public.some_table to authenticated;
  end if;
end $$;
```

This prevents missing optional objects from breaking the run.

## Storage RLS

Private storage buckets should remain private.

For K-FLO roofing documents:

- bucket: `roofing-documents`
- public: false
- object path should start with workspace id
- policies should check workspace membership
- do not allow broad authenticated access across workspaces

Storage path example:

```text
workspace_id/local/9010/document_id/safe-file-name.pdf
```

If storage upload fails with:

```text
new row violates row-level security policy
```

check:

- bucket exists
- storage policies exist
- path starts with workspace id
- path parser helper returns workspace id
- signed-in user belongs to workspace

## Do Not

- Do not make buckets public to fix upload errors.
- Do not grant anon access to workflow tables.
- Do not give authenticated TRUNCATE/TRIGGER/REFERENCES on app tables.
- Do not weaken RLS to make a smoke test pass.
- Do not edit generated `database.types.ts` by hand.

## Report Format

```text
Migration reviewed:
- ...

Grants added:
- ...

RLS changed:
- yes/no

Anon exposure:
- none / intentional list

Verification SQL:
- ...

Safe to apply:
- yes/no, with reason
```
