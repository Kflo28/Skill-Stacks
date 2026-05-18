# K-FLO Communication Drafts Skill

## Purpose

Use this skill when K-FLO drafts customer, crew, agent, manager, or internal communication.

The goal is to produce useful drafts that are vertical-safe, context-aware, approval-gated, and honest about current workflow state.

## Core Rules

- K-FLO drafts. The user approves.
- Never auto-send.
- Never fake a sent message.
- Never include private document links unless the system explicitly supports a safe controlled link.
- Never claim approval, completion, payment, or delivery unless state confirms it.
- Keep customer-facing language calm, clear, and short.
- Keep internal crew/manager language operational and precise.

## Draft Types

Supported draft categories:

- roofing customer update
- roofing change order approval request
- roofing crew notice
- roofing work hold notice
- roofing review request
- roofing closeout update
- insurance client follow-up
- insurance retention/check-in message
- insurance route/callback message
- internal manager summary

## Output Pattern

When presenting a draft, include:

```text
Draft ready for review.
No message has been sent.

To:
Subject:
Body:
```

If send transport is unavailable, say:

```text
Send is unavailable in this mode. Copy Draft is available.
```

## Roofing Customer Update

Use when the customer needs a project status update.

Template:

```text
Subject: Quick update on your roofing project - [Customer]

Hi [Customer],

Quick update on your roofing project.

[Plain-language current state]

We’ll keep you posted if anything affects timing, scope, or approval.

Thanks,
[Rep/Company]
```

Do not mention internal blockers in a scary way. Translate internal state into customer-safe language.

## Roofing Change Order Approval Request

Use only when approval is actually needed.

Template:

```text
Subject: Change Order Approval Needed - [Project/Customer]

Hi [Customer],

During the job-site check, we identified a change to the approved scope:

[Change Order Title]

[Notes]

Related work:
[Related Work]

Estimated amount:
[Amount]

Please reply APPROVED before this portion of work proceeds.

Until approval is received, related work will remain on hold.

Thank you,
[Rep/Company]
```

## Roofing Crew Notice

Use only after approval is received.

Template:

```text
Subject: Change Order Approved - [Project/Customer]

The change order for [Project/Customer] has been approved.

Approved work:
[Related Work]

Notes:
[Notes]

Amount:
[Amount]

Status:
Green light to proceed with the approved related work only.

Do not perform work outside this approved scope without another change order.
```

## Roofing Work Hold Notice

Use when related work must stay held.

```text
Subject: Work Hold - [Project/Customer]

Related work is currently on hold pending approval.

Held work:
[Related Work]

Reason:
[Status/Reason]

Do not release this work until K-FLO shows approval received.
```

## Roofing Review Request

Use only when closeout/review state supports it.

```text
Subject: Thank you for choosing us - quick review request

Hi [Customer],

Thank you again for trusting us with your roofing project.

If you are happy with the work, would you be willing to leave us a quick Google review? It helps future customers know what to expect and helps our crew more than you know.

[Review Link Placeholder]

Thanks again,
[Company/Rep]
```

If no review link is configured, say so instead of inventing one.

## Insurance Follow-Up

```text
Subject: Quick follow-up

Hi [Client],

I wanted to follow up and make sure you had everything you needed from our last conversation.

If you have questions or want to review the next step, I’m happy to help.

Thanks,
[Agent]
```

## Insurance Retention / Review

```text
Subject: Quick coverage check-in

Hi [Client],

I wanted to check in and make sure your current coverage still lines up with your needs.

If anything has changed recently, we can do a quick review and make sure everything is still in good shape.

Thanks,
[Agent]
```

## Wrong-Vertical Guard

If active vertical is roofing, do not use:

- annual coverage review
- policy review
- premium review
- beneficiary review

unless the user explicitly asks about an insurance claim/adjuster context.

If active vertical is insurance, do not use:

- job site
- crew
- change order
- materials
- closeout

unless explicitly relevant.

## Approval and Send Gates

Before any real send:

- recipient must be visible
- subject/body must be visible and editable
- user must explicitly approve
- send mode must be live/live_test if configured
- server-side send path must enforce approval

If any requirement is missing, keep draft/copy-only.

## Quality Check

Before returning a draft:

1. Is this the correct vertical?
2. Is the draft based on actual state?
3. Did I avoid overclaiming?
4. Did I avoid exposing private links?
5. Did I clearly say no message has been sent?
6. Is the next user action obvious?