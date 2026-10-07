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
6. **Discover the full runtime capability surface live.** Static Skill text owns stable selection policy and patterns; current manifests/status own tool names, schemas, providers, readiness, and newly added capabilities.
7. **Persist recoverable state when recovery matters.** Record objective, phase, active work identities, evidence/results, resources, last verified state, exact next action, and decision blockers in an appropriate durable store.
8. **Preserve evidence.** Failed formal evidence remains failed history. Do not alter thresholds, denominators, retries, or source scope merely to convert FAIL to PASS.
9. **Pull results back to the user.** Terminal/resolved backend state is not the same as substantive result delivery.
10. **Respect ownership boundaries.** Project-local contracts and domain Skills own domain truth and quality methods; this Skill owns WebCodex control semantics.
11. **Use topology only when it buys real isolation or concurrency.** Default to one controller. Add workers, integrators, auditors, waits, durable Agents, or multiple Runners only when their separate identity/authority/evidence boundaries materially help.
12. **Placement is a control decision.** Choose a Runner/surface from current authority, project/data locality, platform/capability requirements, resource availability, and recovery cost; never infer placement from convenience alone.

## Core controller loop

For substantial work, use:

~~~text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
~~~

### OBSERVE

Resolve only the state needed for the next decision:

- exact Project and relevant durable run identity;
- exact Session/Goal/Task/Attempt/Job/resource identities already known;
- freshness/generation/fence/snapshot selectors required by the next operation;
- authority and current capability/provider/Host readiness;
- Runner placement and resource ownership when multiple execution locations are possible;
- last verified evidence and project-owned handoff state.

Do not broadly rediscover the project when a valid checkpoint/handoff already identifies the needed delta.

### RECONCILE

Before creating replacement work, determine whether the intended effect already started, completed, failed, or remains unknown.

Uncertain outcome means **observe the same identity first**, not retry blindly.

For parallel work, reconcile each exact Task/Attempt/Job and the integration candidate rather than collapsing worker claims into one synthetic status.

### ACT

Perform one bounded authorized effect using current identity/freshness/authority. Acquire or attach only resources needed for that effect.

If the objective itself is missing or ambiguous, do not create speculative work.

Fan out only work that can be assigned with clear ownership, dependencies, result contract, and integration/audit path.

### VERIFY

Re-observe enough state to establish what actually changed. Treat state-changing Browser/Computer operations, fenced assignments, Task attempts, Job handoffs, Endpoint generations, file revisions, and other generation-bound operations as freshness boundaries.

Worker completion is not integration proof. Integration success is not independent audit proof.

### PERSIST / HANDOFF

When recovery matters, persist:

- current objective and phase/status;
- active exact identities and dependency/topology state;
- Runner/surface placement when relevant;
- evidence/result/artifact locations;
- resource ownership;
- last verified state;
- integration/audit state when applicable;
- exact next allowed action;
- real decision blockers.

Then continue automatically while the objective and authority remain clear, or stop at a true decision boundary.

## WebCodex-native composition

Use the smallest topology that satisfies the task:

~~~text
single controller
or
supervisor -> workers -> optional integrator -> independent auditor
~~~

Use durable Goal/Agent/AgentTask/Attempt/AgentWait/continuation primitives only when live runtime readiness supports them. API exposure alone is insufficient.

Prefer event-driven waits/continuation over repeated polling when a supported durable wake path exists. If no wake-capable path is ready, persist the exact continuation state and recover it in a later turn.

For multi-Runner work, place execution explicitly. For cross-Project work, move artifacts through verified handoff/transfer paths rather than through model text when the runtime provides them.

## References

- For the generic control model and bounded execution semantics, read [references/execution-model.md](references/execution-model.md).
- For cross-domain durable run state, read [references/durable-run-state.md](references/durable-run-state.md).
- For Project Driver versus domain/project ownership, read [references/composition-boundaries.md](references/composition-boundaries.md).
- For interruption and uncertain-outcome recovery, read [references/interruption-recovery.md](references/interruption-recovery.md).
- For long Jobs, async/detached processes, and persistent shells, read [references/long-running-work.md](references/long-running-work.md).
- For controller/worker/integrator/auditor topologies, AgentTask/Attempt, and fan-out/fan-in, read [references/orchestration.md](references/orchestration.md).
- For multi-Runner/fleet placement, read [references/runner-placement.md](references/runner-placement.md).
- For Agent/Job waits, Endpoint/Wake readiness, and automatic continuation, read [references/event-driven-continuation.md](references/event-driven-continuation.md).
- For Browser, Computer, SSH, artifacts, and cross-Project operations, read [references/cross-surface-operations.md](references/cross-surface-operations.md).
- For autonomous remediation, escalation, and human decision boundaries, read [references/autonomy-escalation.md](references/autonomy-escalation.md).
- For evidence, verification, failure preservation, integration, and independent control-plane review, read [references/validation-audit.md](references/validation-audit.md).
- For phase closeout, handoff, resources, and retrospective, read [references/closeout-retrospective.md](references/closeout-retrospective.md).
- For full live capability discovery, extension surfaces, and downgrade behavior, read [references/webcodex-capabilities.md](references/webcodex-capabilities.md).
- For Git/worktree/commit behavior when Git is an authoritative software-project substrate, read [references/software-git-adaptation.md](references/software-git-adaptation.md).

## Decision boundaries

Stop for genuine decisions such as:

- the objective or next authorized action is materially ambiguous;
- a frozen project architecture/scope/acceptance contract must change;
- accepting a material unresolved risk instead of satisfying a required gate;
- destructive cleanup or history rewrite;
- protected/default-branch promotion or release when project policy reserves that decision;
- irreversible external action not already authorized;
- missing authority or unavailable capability that materially changes the plan.

Do not stop for routine observation, bounded authorized execution, supported worker dispatch, continued observation of an already-started Job/Task, evidence persistence, safe remediation inside the frozen contract, or non-destructive recovery mechanics.

## Recovery invariant

After interruption or uncertain delivery, recover exact identity and verified evidence first, then continue only the uncompleted delta. Never equate a browser/chat window, recent activity, a stale selector, or a worker's claim with durable task truth.
