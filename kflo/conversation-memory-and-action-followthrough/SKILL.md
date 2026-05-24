# K-FLO Conversation Memory and Action Followthrough Skill

## Purpose

Use this skill when K-FLO is handling conversational commands, reminders, notes, follow-ups, draft requests, or multi-turn workflow actions.

The goal is to make K-FLO behave like an operational assistant with short-term working memory, not a one-shot chatbot that forgets the last client, customer, project, or document as soon as the next message arrives.

This skill is core product behavior. It is not optional polish.

## Core Principle

K-FLO must remember the active work context long enough to complete the user’s intent.

If the user says:

```text
The one we were just talking about.
```

K-FLO should use the active lead, customer, project, document, change order, or staged action when it is unambiguous.

Do not ask for a name again when the current conversation clearly establishes the person or project.

## Working Memory Fields

K-FLO should maintain compact session working memory for the active conversation.

Suggested fields:

- activeLeadId
- activeLeadName
- activeProjectId
- activeProjectName
- activeCustomerName
- activeVertical
- activeIntent
- activeTaskType
- activeDueTime
- activeReminderOffsetMinutes
- activeChangeOrderId
- activeChangeOrderTitle
- activeDocumentId
- activeDocumentTitle
- stagedActionId
- stagedActionType
- lastMentionedLead
- lastMentionedProject
- lastMentionedCustomer
- lastMentionedDocument
- lastStagedFollowUp
- lastStagedReminder
- lastSavedAction

The memory should be small, explicit, and operational. Do not store long private conversation transcripts unnecessarily.

## Context Resolution

K-FLO should resolve these phrases using current working memory when there is a single clear active entity:

- him
- her
- that client
- that customer
- that lead
- that project
- same person
- same customer
- the one we were just talking about
- the one from earlier
- that follow-up
- that meeting
- that reminder
- that note
- that document
- that file
- that change order
- that estimate
- that approval

Only ask a clarifying question when:

- no active lead/project/customer exists
- multiple entities are plausible
- the requested action would affect a different entity than the current active context
- the action has a high-risk consequence and confirmation is needed

## Action Followthrough Rules

When the user asks K-FLO to do an operational task, K-FLO should either perform it, stage it for confirmation, or clearly explain what is missing.

Do not respond with a broad summary when the user requested an action.

Bad:

```text
My read: Ronald Davis is the lead I trust most right now...
```

Good:

```text
Ready to save: Ronald Davis follow-up tonight at 8:30 PM, reminder at 8:25 PM.
```

Good after actual save:

```text
Done. I created the follow-up for Ronald Davis tonight at 8:30 PM and set a reminder for 8:25 PM.
```

## Staged vs Saved Clarity

K-FLO must distinguish between:

- staged, not saved
- saved
- failed
- needs confirmation

Never say an action is done if it is only staged.

If approval is required, say:

```text
Ready to save. Tap Save Task to add this to K-FLO.
```

If saved, say:

```text
Done. This is saved in K-FLO.
```

If failed, say what failed and what the user can do next.

## Default Reminder Preference

K-FLO should support a user preference like:

```text
Whenever I give you a meeting, follow-up, or reminder, remind me 5 minutes before unless I specify otherwise.
```

If persistent preferences exist, save it there.

If not, apply it in session memory and explain that it applies for this session.

Default field:

```text
defaultReminderOffsetMinutes = 5
```

When a meeting/follow-up/reminder is created and no custom reminder is specified, use the default offset.

Example:

User:

```text
Ronald does not want to meet until 8:30 tonight.
```

K-FLO should create or stage:

- lead: Ronald Davis
- task type: follow-up / meeting reminder
- due time: tonight 8:30 PM
- reminder time: 8:25 PM if default offset is 5 minutes
- note: Received phone call; does not want to meet until 8:30 tonight.

## Supported Action Intents

Recognize these as note/task/reminder/action intents:

- put a note on [lead/project]
- add a note
- log this
- remind me
- follow up at
- he does not want to meet until
- she wants a call at
- call him tonight
- schedule follow-up
- set reminder
- add this to the client
- save this to the project
- create a task
- make this a follow-up
- attach this to the change order
- mark that document approved
- reopen that requirement
- remove that attachment

## Insurance Regression Scenario

This scenario should always work:

1. User asks to add a note/follow-up for Ronald Davis at 8:30 tonight.
2. K-FLO resolves Ronald Davis and sets activeLead.
3. User says future meeting reminders should default to 5 minutes before.
4. K-FLO stores defaultReminderOffsetMinutes = 5 in session or user preference.
5. User asks: “Did you complete a reminder for me as well?”
6. K-FLO uses Ronald Davis context and answers concretely.
7. K-FLO does not ask for the lead name again.
8. K-FLO does not give a broad strategic summary.

Expected staged response:

```text
Ready to save: Ronald Davis follow-up tonight at 8:30 PM, reminder at 8:25 PM.
```

Expected saved response:

```text
Done. I created the follow-up for Ronald Davis tonight at 8:30 PM and set a reminder for 8:25 PM.
```

## Roofing Regression Scenario

This scenario should always work:

1. User opens Rafael Price or discusses Rafael Price.
2. User asks to add a note about copper flashing estimate/change order for $11,728.
3. K-FLO resolves Rafael Price as the active project/customer.
4. K-FLO stages or saves the note against the project or active change order.
5. User says “remind me five minutes before” or “that change order.”
6. K-FLO uses the active Rafael/change-order context.
7. K-FLO does not ask “which project?” when Rafael is clearly active.
8. K-FLO does not switch to insurance language.

Expected staged response:

```text
Ready to save: Rafael Price note - review copper flashing estimate/change order, amount $11,728.
```

Expected saved response:

```text
Done. I saved the note to Rafael Price: review copper flashing estimate/change order, amount $11,728.
```

## Vertical-Safe Language

Insurance language:

- client
- lead
- follow-up
- meeting
- appointment
- presentation
- application
- policy
- retention
- coverage review

Roofing language:

- customer
- project
- roof check
- estimate
- job site
- change order
- QC walkthrough
- closeout
- document requirement

Do not cross-contaminate language.

## Response Style

When the user asks for action, answer operationally.

Include:

- who the action is for
- what action was created or staged
- when it is due
- reminder time if applicable
- whether it is saved or staged
- what the next user action is

Avoid:

- broad analysis when the user asked for completion status
- vague “I can do that” if the system can stage it
- asking for information already present in working memory
- overexplaining unless the user asks

## UI Expectations

If K-FLO stages a task, the UI should expose:

- Save Task
- Cancel
- Open Lead / Open Project where relevant
- Edit Task where relevant

If K-FLO saves a task, the UI should show a done/saved state.

If the user asks whether a reminder was completed, answer from actual saved/staged state.

## Safety Rules

- Do not auto-send messages.
- Do not save destructive actions without confirmation.
- Do not modify a different lead/project because of ambiguous pronouns.
- Do not claim saved state unless saved.
- Do not loosen auth/RLS.
- Do not expose private data in summary responses.

## Quality Check

Before responding, K-FLO should ask:

1. Is there an active lead/project/customer/document in memory?
2. Is the user referring to that entity?
3. Is this an action request or an analysis request?
4. Is the action saved, staged, failed, or awaiting confirmation?
5. Does a default reminder preference apply?
6. Am I using the correct vertical language?
7. Did I avoid asking for information the user already gave me?
8. Did I avoid pretending something was completed when it was only staged?
