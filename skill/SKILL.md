---
name: webcodex-project-driver
description: Operate WebCodex-specific durable control semantics for stateful execution. Use when ChatGPT must address exact WebCodex Projects, Runners, Sessions, Goals, Tasks/Attempts, Jobs, resources, surfaces, artifacts, waits/wakes, freshness/fence/generation state, uncertain WebCodex effects, Runner placement, or live runtime capability readiness. It may co-activate with agent-operating-model for generic scope, proportional-rigor, recovery, verification, and authority guardrails. Do not use it as a generic project, coding, research, or software-development methodology Skill.
---

# WebCodex Project Driver

Treat WebCodex as the durable execution/control plane. Keep this Skill at the platform-semantics layer: project-local instructions own project truth, domain Skills own domain methods, and `agent-operating-model` owns generic scope/process/recovery/authority guardrails when that Skill is active.

## Core invariants

1. **Identity, freshness, and authority are separate.** For a WebCodex effect, distinguish the durable object being addressed from its current fence/generation/snapshot/attempt proof and from the authority that permits the effect.
2. **Observe live WebCodex state before platform mutation.** Use exact Projects/Runners/Sessions/Tasks/Jobs/resources and current manifests/status rather than chat position, recency, or assumed runtime configuration.
3. **Reconcile uncertain WebCodex effects before retry.** If a prior Session/Task/Job/resource/action may already exist, inspect that same identity or replay/idempotency key before replacement dispatch.
4. **Capability exposure is not readiness.** Current manifests/status own tool schemas, provider inventory, Host continuation readiness, and Runner capabilities.
5. **Keep platform lifecycle states distinct.** Worker completion, integration state, audit state, wake delivery, and user-visible result delivery are different facts.
6. **Pull substantive results back.** A terminal Job/Task/Session is not the same as delivering its result/artifact to the user or next controller.
7. **Make Runner placement explicit when it matters.** Bind execution to the Runner/surface that actually satisfies authority, locality, platform, capability, and lifecycle requirements.
8. **Track WebCodex resource and scratch ownership.** Keep borrowed/owned resources and Runner-local recoverable scratch tied to exact Project/run identities until safely handed off or released.
9. **Make attention recoverable before presentation.** Reconcile source Task/Job/audit state before relying on Wake, Host re-entry, or notification delivery.
10. **Respect composition boundaries.** This Skill owns WebCodex control semantics only; do not duplicate repository policy, domain methodology, or generic operating-model rules.

## WebCodex control loop

For a stateful WebCodex effect, use:

~~~text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
~~~

### OBSERVE

Resolve only the WebCodex state needed for the next platform decision:

- exact Project/Runner and relevant Session/Goal/Task/Attempt/Job/resource identities;
- freshness/generation/fence/snapshot selectors required by the next call;
- current provider/capability/Host readiness;
- Runner/surface placement and resource ownership when relevant;
- last verified control-plane evidence/handoff.

A valid checkpoint should narrow observation; do not rediscover the entire project merely because a new model turn began.

### RECONCILE

Before replacement dispatch, determine whether the exact prior effect started, completed, failed, remains active, or is still unknown.

For parallel work, reconcile each exact Task/Attempt/Job and the integration candidate separately.

### ACT

Perform the next authorized WebCodex effect using current identity/freshness/authority. Attach only the platform resources required for that effect.

When workers are already justified by the outer task contract, give each exact ownership, dependencies, output/evidence contract, and integration destination.

### VERIFY

Re-observe the affected WebCodex state. Treat Browser/Computer navigation, fenced assignments, Task attempts, Job handoffs, Endpoint generations, file revisions, and other generation-bound operations as freshness boundaries.

Do not treat command dispatch, worker claims, wake delivery, or artifact transport as proof of the higher-level result they support.

### PERSIST / HANDOFF

When recovery/handoff is required by the outer task contract, persist the WebCodex-specific fields needed to resume safely:

- exact active identities and dependency/topology state;
- Runner/surface placement;
- freshness selectors that remain reusable;
- evidence/result/artifact locations and provenance;
- resource/scratch ownership and cleanup state;
- pending wait/wake/attention state;
- last verified platform state;
- exact next WebCodex observation/effect.

The outer project or `agent-operating-model` owns the generic objective, scope, decision gates, and whether durable recovery state is needed.

## WebCodex-native composition

Topology choice is governed by the actual task contract and generic operating model. Once a topology is justified, this Skill owns its WebCodex mechanics:

~~~text
single controller
or
controller -> workers -> optional integrator -> optional auditor
~~~

Use Goal/Agent/AgentTask/Attempt/AgentWait/continuation primitives only when current runtime readiness supports them. API exposure alone is insufficient.

Prefer event-driven waits/continuation over repeated polling when a supported durable wake path is ready. If no wake-capable path is ready, preserve exact identities/state for later recovery.

For multi-Runner work, place execution explicitly. For cross-Project work, move artifacts through verified runtime handoff/transfer paths rather than model text when available.

## References

- For WebCodex identity/freshness/resource control semantics, read [references/execution-model.md](references/execution-model.md).
- For WebCodex-specific recovery fields to add to an outer durable handoff, read [references/durable-run-state.md](references/durable-run-state.md).
- For ownership with project instructions, domain Skills, and `agent-operating-model`, read [references/composition-boundaries.md](references/composition-boundaries.md).
- For interruption and uncertain WebCodex outcome recovery, read [references/interruption-recovery.md](references/interruption-recovery.md).
- For Jobs, async/detached processes, and persistent shells, read [references/long-running-work.md](references/long-running-work.md).
- For Task/Attempt/Wait and controller/worker/integrator/auditor mechanics, read [references/orchestration.md](references/orchestration.md).
- For multi-Runner placement, read [references/runner-placement.md](references/runner-placement.md).
- For Agent/Job waits, Endpoint/Wake readiness, and Host continuation, read [references/event-driven-continuation.md](references/event-driven-continuation.md).
- For Browser, Computer, SSH, artifacts, and cross-Project operations, read [references/cross-surface-operations.md](references/cross-surface-operations.md).
- For Runner-local temporary file ownership and cleanup, read [references/scratch-lifecycle.md](references/scratch-lifecycle.md).
- For durable completion/failure/interruption attention delivery, read [references/attention-routing.md](references/attention-routing.md).
- For WebCodex-specific failure routing and capability blockers, read [references/autonomy-escalation.md](references/autonomy-escalation.md).
- For control-plane evidence provenance, integration, and audit semantics, read [references/validation-audit.md](references/validation-audit.md).
- For WebCodex resource/identity closeout, read [references/closeout-retrospective.md](references/closeout-retrospective.md).
- For live capability discovery and safe downgrade, read [references/webcodex-capabilities.md](references/webcodex-capabilities.md).
- For Git mapping and WebCodex-managed worktree selection/reuse/cleanup, read [references/software-git-adaptation.md](references/software-git-adaptation.md).

## WebCodex-specific blockers

Use the outer user/project/platform contract for generic scope, risk, release, and destructive-action decisions. This Skill adds platform blockers when, for example:

- the exact target Project/Runner/Session/Task/Job/resource cannot be identified safely;
- a required fence/generation/snapshot is stale and cannot be refreshed;
- a prior WebCodex effect remains outcome-unknown and duplicate execution would be unsafe;
- a required provider/capability/Host path is unavailable with no equivalent verified fallback;
- Runner/resource ownership is unresolved and moving/duplicating work could corrupt or duplicate state.

Do not invent additional approval gates merely because a WebCodex primitive exists.

## Recovery invariant

After interruption or uncertain delivery, recover exact WebCodex identity and verified platform evidence first, then continue only the unresolved platform delta. Never equate a chat/browser window, recent activity, stale selector, wake delivery, or worker claim with durable execution truth.
