# Execution Model

## Scope

This reference defines **WebCodex control-plane state**, not a generic project workflow. The outer user/project contract or `agent-operating-model` owns objective scope, proportional rigor, generic recovery policy, and material decision boundaries.

## WebCodex state model

Keep these concerns separate:

- **durable identity**: Project, Runner, Session, Goal, Agent, Task/Attempt, Job, resource, artifact, surface, or delegated-run identity;
- **freshness/generation proof**: fence, Attempt/Endpoint generation, snapshot/ref, observation token, replay/idempotency selector, file revision, or equivalent;
- **effect authority**: current WebCodex/project permission for the platform effect;
- **control-plane evidence**: what state transition was actually re-observed;
- **resource ownership**: borrowed/owned, persistent/ephemeral, Runner/locality, release/handoff expectations;
- **presentation**: the current ChatGPT/Host turn or notification path.

Never silently substitute one for another.

## Takeover or continuation

When resuming WebCodex-backed work:

1. resolve the exact Project/Runner context required by the next effect;
2. recover known Session/Goal/Task/Attempt/Job/resource identities rather than inferring from recency;
3. read the last durable handoff needed to identify unresolved WebCodex state;
4. refresh fence/generation/snapshot proof only when the next call requires it;
5. discover current provider/capability/Host readiness for optional paths;
6. reconcile only the unresolved platform delta.

If the outer objective or allowed next action is unclear, defer that decision to the applicable project instructions or `agent-operating-model`; do not manufacture a WebCodex task to create motion.

## WebCodex control loop

~~~text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
~~~

### Observe

Read enough exact runtime state to choose the next platform action.

### Reconcile

If earlier execution may already exist, inspect that exact identity before replacement dispatch. Reuse idempotency/replay selectors according to the live runtime contract.

### Act

Execute the authorized WebCodex effect with current identity/freshness/authority.

### Verify

Re-observe the affected platform state and preserve explicit uncertainty when the outcome cannot yet be proven.

### Persist / handoff

When the outer task requires recovery/handoff, persist the WebCodex-specific identity, freshness, resource, placement, evidence, and continuation fields needed to resume safely. See [durable-run-state.md](durable-run-state.md).

## Resource lifecycle

Track important WebCodex-controlled resources through:

~~~text
ACQUIRE / ATTACH
-> USE
-> RECONCILE / VERIFY
-> HANDOFF or RELEASE
-> FAILURE CLEANUP
~~~

Do not destroy unique evidence or recovery state during cleanup.

## Continuation

Whether work should continue automatically is an outer task/authority decision. This Skill only supplies the platform facts required for that decision:

- exact current identity/state;
- whether the prior effect is reconciled;
- whether required capability/provider/Host readiness exists;
- whether resource ownership and freshness permit the next effect;
- whether a WebCodex-specific blocker remains.
