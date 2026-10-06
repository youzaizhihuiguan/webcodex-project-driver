---
name: webcodex-project-driver
description: Drive substantial stateful work through WebCodex as a durable control plane. Use when ChatGPT must execute, continue, recover, or coordinate work whose real state lives in WebCodex projects, Sessions, Jobs, Goals/Tasks, resources, evidence, or handoffs across multiple steps or model turns. Keep exact identity, freshness/generation proof, authority, reconciliation, verification, and durable next-action state separate. Do not use it as a generic domain-methodology Skill or as permission to invent work when the user's objective is ambiguous.
---

# WebCodex Project Driver

Treat WebCodex as the durable execution/control plane and the current model turn as disposable.

## Core invariants

1. **Identity, freshness, authority are separate.** Before a stateful effect, know the durable object being addressed, the current fence/generation/snapshot/attempt proof when required, and the authority that permits the effect.
2. **Observe real state before acting.** Use WebCodex and authoritative project artifacts, not chat memory, tab position, or assumed runtime configuration.
3. **Reconcile uncertain outcomes before retry.** If prior work may already exist, inspect the exact existing Session/Task/Job/resource or replay key before dispatching replacement work.
4. **Ambiguous objective is not permission to invent work.** Do not infer a new write task, evidence artifact, branch, push, experiment, or external mutation merely from repository/project contents. Preserve state and treat the missing objective/next action as a decision blocker unless an authoritative project contract already defines it.
5. **Keep execution bounded.** Use short model batches that can finish, verify, persist, or hand off without making one reply carry an entire long-running stage.
6. **Discover volatile runtime contracts live.** Use current WebCodex manifests/status/capability observations for tool schemas, providers, Host continuation, Browser/Computer, SSH, plugins, LSP, and other optional backends. Static Skill text owns stable policy, not volatile schemas.
7. **Persist recoverable state when recovery matters.** Record objective, phase, active work identities, evidence/results, resources, last verified state, exact next action, and decision blockers in an appropriate durable store.
8. **Preserve evidence.** Failed formal evidence remains failed history. Do not alter thresholds, denominators, retries, or source scope merely to convert FAIL to PASS.
9. **Pull results back to the user.** Terminal/resolved backend state is not the same as substantive result delivery.
10. **Respect ownership boundaries.** Project-local contracts and domain Skills own domain truth and quality methods; this Skill owns WebCodex control semantics.

## Core controller loop

For substantial work, use:

```text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
```

### OBSERVE

Resolve only the state needed for the next decision:

- exact Project and relevant durable run identity;
- exact Session/Goal/Task/Job/resource identities already known;
- freshness/generation/fence/snapshot selectors required by the next operation;
- authority and current optional capability readiness;
- last verified evidence and project-owned handoff state.

Do not broadly rediscover the project when a valid checkpoint/handoff already identifies the needed delta.

### RECONCILE

Before creating replacement work, determine whether the intended effect already started, completed, failed, or remains unknown.

Uncertain outcome means **observe the same identity first**, not retry blindly.

### ACT

Perform one bounded authorized effect using current identity/freshness/authority. Acquire or attach only resources needed for that effect.

If the objective itself is missing or ambiguous, do not create speculative work.

### VERIFY

Re-observe enough state to establish what actually changed. Treat state-changing Browser/Computer operations, fenced assignments, Task attempts, Job handoffs, and other generation-bound operations as freshness boundaries.

### PERSIST / HANDOFF

When recovery matters, persist:

- current phase/status;
- active exact identities;
- evidence/result locations;
- resource ownership;
- last verified state;
- exact next allowed action;
- real decision blockers.

Then continue automatically while the objective and authority remain clear, or stop at a true decision boundary.

## References

- For the generic control model and bounded execution semantics, read [references/execution-model.md](references/execution-model.md).
- For cross-domain durable run state, read [references/durable-run-state.md](references/durable-run-state.md).
- For Project Driver versus domain/project ownership, read [references/composition-boundaries.md](references/composition-boundaries.md).
- For interruption and uncertain-outcome recovery, read [references/interruption-recovery.md](references/interruption-recovery.md).
- For long Jobs, async/detached processes, and persistent shells, read [references/long-running-work.md](references/long-running-work.md).
- For multi-Session/Goal/AgentTask/AgentWait orchestration, read [references/orchestration.md](references/orchestration.md).
- For evidence, verification, failure preservation, and independent control-plane review, read [references/validation-audit.md](references/validation-audit.md).
- For phase closeout, handoff, resources, and retrospective, read [references/closeout-retrospective.md](references/closeout-retrospective.md).
- For live capability discovery and downgrade behavior, read [references/webcodex-capabilities.md](references/webcodex-capabilities.md).
- For Git/worktree/commit behavior when Git is an authoritative software-project substrate, read [references/software-git-adaptation.md](references/software-git-adaptation.md).

## Decision boundaries

Stop for genuine decisions such as:

- the objective or next authorized action is materially ambiguous;
- a frozen project architecture/scope/acceptance contract must change;
- accepting a material unresolved risk instead of satisfying a required gate;
- destructive cleanup or history rewrite;
- protected/default-branch promotion when project policy reserves that decision;
- missing authority or unavailable capability that materially changes the plan.

Do not stop for routine observation, bounded authorized execution, continued observation of an already-started Job, evidence persistence, or non-destructive recovery mechanics.

## Recovery invariant

After interruption or uncertain delivery, recover exact identity and verified evidence first, then continue only the uncompleted delta. Never equate a browser/chat window, recent activity, or a stale selector with durable task identity.
