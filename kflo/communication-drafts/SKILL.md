# K-FLO Communication Drafts Skill

## Purpose

Use this skill when K-FLO drafts customer, crew, agent, manager, or internal communication.

The goal is to produce useful drafts that are vertical-safe, context-aware, approval-gated, and honest about current workflow state.

This skill is a communication logic layer, not just a copywriting helper. It tells K-FLO when a message is appropriate, when it is redundant, and what business event should trigger the draft.

## Core Rules

- K-FLO drafts. The user approves.
- Never auto-send.
- Never fake a sent message.
- Never include private document links unless the system explicitly supports a safe controlled link.
- Never claim approval, completion, payment, warranty, delivery, or customer contact unless state confirms it.
- Keep customer-facing language calm, clear, and short.
- Keep internal crew/manager language operational and precise.
- Do not create a customer update just because an internal status changed.
- Tie every customer update to a specific customer-facing reason.
- If the reason is internal-only, keep it internal.

## Draft Types

Supported draft categories:

- roofing customer update
- roofing quality-control walkthrough request
- roofing change order approval request
- roofing crew notice
- roofing work hold notice
- roofing review request
- roofing referral request
- roofing marketing/photo permission request
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

## Customer Update Trigger Logic

Do not use generic “Customer updated” as a standalone requirement without a reason.

Customer updates should be trigger-based. K-FLO should be able to explain why the customer needs an update.

### Valid Roofing Customer Update Triggers

Use a customer update when the customer-facing situation has changed or needs action:

- schedule change
- material delay
- weather delay
- crew arrival/time change
- change order approval needed
- major scope discovery
- job delayed or blocked
- work completed and quality-control walkthrough needs scheduling

### Do Not Automatically Trigger Customer Updates For

These are internal or already-communicated states and should not create a generic customer update by themselves:

- change order approved
- closeout started
- final documents ready
- internal closeout status changes
- review request prepared
- warranty notes added

Change order approved should not automatically create a new customer update requirement because customer approval already implies customer communication occurred.

Final documents ready is usually internal until the user explicitly wants to send a final packet.

Closeout started is internal and should not trigger a customer-facing message by itself.

## Roofing Customer Update

Use when the customer needs a project status update because of a customer-facing trigger.

Template:

```text
Subject: Quick update on your roofing project - [Customer]

Hi [Customer],

Quick update on your roofing project.

[Plain-language current state tied to the trigger]

We’ll keep you posted if anything affects timing, scope, or approval.

Thanks,
[Rep/Company]
```

Do not mention internal blockers in a scary way. Translate internal state into customer-safe language.

Do not say work is complete unless the workflow state supports it.

## Roofing Quality-Control Walkthrough Request

Use when work is completed and the next customer-facing step is a QA/QC walkthrough.

This is the preferred customer-facing draft after work completion. Do not simply say “work is done” without giving the customer a next step.

Template:

```text
Subject: Quality-control walkthrough for your roofing project - [Customer]

Hi [Customer],

The main work on your roofing project is complete. The next step is a quick quality-control walkthrough so we can make sure everything is buttoned up properly.

What time works best for you to walk through it with us?

Thanks,
[Rep/Company]
```

Use “quality-control walkthrough,” “QC walkthrough,” or “final walkthrough” depending on the company’s preferred wording.

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

## Roofing Referral Request

Use only when the user has marked the customer as a referral fit or asks for a referral draft.

Template:

```text
Subject: Quick favor after your roofing project

Hi [Customer],

Thank you again for trusting us with your roofing project.

If you know a neighbor, friend, or family member who may need a roof inspection or help with storm-related roof concerns, we would be grateful for the referral.

We’ll take good care of anyone you send our way.

Thanks again,
[Rep/Company]
```

If the customer is not a referral fit, do not draft this automatically. Capture the note explaining why.

## Roofing Marketing / Photo Permission Request

Use when the company wants permission to use project photos, before/after images, testimonial language, or marketing material.

Template:

```text
Subject: Permission to use project photos

Hi [Customer],

Would you be comfortable with us using a few photos from your roofing project in our marketing or project examples?

We would not share your personal contact information, and we can avoid showing anything you do not want shown.

Please reply and let us know if that is okay, or if there are any restrictions you would like us to follow.

Thanks,
[Rep/Company]
```

K-FLO should track:

- marketing photo permission requested
- permission granted
- permission declined
- restrictions or notes
- whether customer name/address may be shown

Do not assume permission because photos were uploaded.

## Roofing Closeout Communication Rules

Closeout is partly internal. Do not generate customer-facing messages for every closeout item.

### Customer-Facing Closeout Messages

Appropriate:

- QC/final walkthrough scheduling
- review request
- referral request
- marketing/photo permission request
- final packet delivery if the user explicitly requests it

### Internal-Only Closeout States

Do not automatically send customer updates for:

- closeout started
- final documents attached
- warranty notes added
- referral opportunity checked
- review request prepared but not ready to send

## Closeout Notes Requirements

When drafting or summarizing closeout state, K-FLO should prefer items with notes. Closeout notes explain what happened for future users.

Examples:

Work completed note:

```text
Ridge vent installed, damaged decking replaced, cleanup complete.
```

Referral note:

```text
Good referral candidate. Neighbor asked about inspection.
```

Not a referral fit note:

```text
Not a referral fit. Customer requested no follow-up beyond warranty.
```

Warranty note:

```text
Manufacturer warranty packet sent.
```

Warranty not applicable note:

```text
Warranty not applicable for repair-only job.
```

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
7. Is the customer update tied to a real customer-facing trigger?
8. Is the message internal-only instead of customer-facing?
9. If it is a closeout message, does it need notes or permission before sending?
