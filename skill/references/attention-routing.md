# Attention Routing

## Purpose

Separate durable project/task truth from the mechanism used to regain model or human attention.

An attention event is a control-plane record that something terminal, blocked, degraded, or decision-relevant occurred. Notification delivery is presentation, not execution truth.

## Contents

- [Event classes](#event-classes)
- [Durable-before-notify rule](#durable-before-notify-rule)
- [Routing](#routing)
- [Completion and interruption](#completion-and-interruption)
- [Channel policy](#channel-policy)
- [Coalescing](#coalescing)
- [Recovery payload](#recovery-payload)
- [Wake is not truth](#wake-is-not-truth)

## Event classes

Use a small stable event vocabulary when useful:

- `TASK_COMPLETED`
- `TASK_FAILED`
- `JOB_COMPLETED`
- `JOB_FAILED`
- `JOB_LOST`
- `RUNNER_OFFLINE`
- `CONTINUATION_UNAVAILABLE`
- `AUDIT_PASS`
- `AUDIT_BLOCKED`
- `USER_DECISION_REQUIRED`

Do not emit an event merely because a model turn ended.

## Durable-before-notify rule

Before relying on a notification or Host wake:

1. reconcile the exact source Task/Job/Runner/audit state;
2. persist enough source identity and last verified state to recover;
3. record the required next action or decision;
4. then attempt attention delivery through a currently available channel.

If delivery fails or no Host carrier is available, the durable event remains pending. The next controller turn must surface/reconcile it instead of inventing replacement work.

## Routing

This reference routes **delivery and controller attention**, not generic project authority.

The user/project contract or `agent-operating-model` decides whether a genuine user decision exists. Once that is known:

### Controller continuation

If the outer contract authorizes continuation, a terminal WebCodex event may wake/resume the controller without adding a new approval gate.

### Supervisor/controller attention

Route to controller reasoning when scheduling, WebCodex remediation, integration, placement, or runtime fallback must be recomputed inside the existing authority.

### Human attention

Surface to the user when the outer contract requires a decision or terminal notification, or when no verified WebCodex fallback can preserve the authorized work.

Do not promote notification delivery itself into a project gate.

## Completion and interruption

When configured by the user, terminal completion should produce a user-visible attention delivery after the final result/evidence is reconciled.

Interruption/degradation should be made recoverable and surfaced when the outer contract requires user awareness or when it prevents any verified platform continuation, including:

- lost Job after reconciliation;
- Runner offline with no safe continuation;
- Host continuation path unavailable when automatic continuation was required;
- repeated failure with no evidence-driven retry;
- blocked audit or required user decision.

A temporary model-turn end with durable recoverable work is not by itself a failure notification.

## Channel policy

Discover notification/presentation capabilities live. Do not hard-code one vendor or assume Push/Email/Slack/webhook availability.

Examples of possible channels include Host wake/presentation, ChatGPT-visible result delivery, OS notification, email, or an authorized external integration.

Sending to an external service is an external effect and must use existing authorization/policy. Do not silently configure a new provider merely to notify.

## Coalescing

Avoid alert storms.

When several exact events belong to the same bounded phase and one consolidated attention record is sufficient, coalesce presentation while preserving each underlying durable source identity/evidence.

Do not coalesce away a failure, blocker, or required decision.

## Recovery payload

A useful pending attention record contains:

- event class;
- exact Project/Runner;
- exact source Task/Attempt/Job/audit identity;
- last verified state;
- result/evidence location;
- whether automatic continuation is possible;
- exact next action or smallest user decision;
- delivery state/channel when known.

## Wake is not truth

AgentWait, Wake, Endpoint continuation, Job terminal attention, and other carriers can re-enter a controller, but none of them replace independent reconciliation of the source state.

Likewise, successful notification delivery does not prove the underlying task succeeded.
