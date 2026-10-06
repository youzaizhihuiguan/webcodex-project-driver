# Execution Model

## Control-plane state model

Treat these as separate concerns:

- **objective**: what the user/project actually authorizes;
- **durable identity**: Project, Session, Goal, Task, Job, resource, artifact, or domain-owned run identity;
- **freshness/generation proof**: fence, attempt generation, snapshot/ref, observation token, replay/idempotency selector, or equivalent;
- **authority**: permission and project policy for the intended effect;
- **evidence**: what has actually been observed or verified;
- **resource ownership**: borrowed/owned, persistent/ephemeral, release/handoff expectations;
- **presentation**: the current ChatGPT turn/window.

Never silently substitute one for another.

## Takeover or continuation

When starting or resuming substantial work:

1. resolve the exact Project or other required WebCodex execution context;
2. recover exact known Session/Goal/Task/Job/resource identities rather than inferring from recency;
3. read the last authoritative durable handoff/evidence needed for the next decision;
4. inspect current freshness/generation proof only when the next action requires it;
5. discover current capability/provider readiness when an optional path is being considered;
6. derive the smallest unfinished authorized delta.

If the objective or exact next action is not actually defined, record that as a decision blocker. Do not mine the repository/project for a speculative task.

## Universal controller loop

```text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
```

### Observe

Acquire enough current state to make the next control decision. Prefer precise targeted reads over broad rediscovery.

### Reconcile

If earlier execution may already exist, determine its state before creating replacement work. Reuse exact identities and replay/idempotency selectors according to the live runtime contract.

### Act

Execute one bounded authorized effect with current identity, freshness proof, and authority.

### Verify

Re-observe the affected state and distinguish intended success, explicit failure, and uncertain outcome.

### Persist / handoff

When recovery matters, persist current state, evidence, resources, and the exact next action. Use the domain/project's authoritative durable store rather than forcing one storage format.

## Bounded action

A useful bounded action normally has:

- one clear objective;
- known current predecessor/state;
- limited effect scope;
- explicit verification;
- a natural persistence/handoff boundary.

A project may continue for hours or days. One model turn should usually run only long enough to decide, execute/dispatch one bounded unit, verify or establish durable state, and return/yield.

## Resource lifecycle

Track important resources through:

```text
ACQUIRE / ATTACH
-> USE
-> VERIFY
-> HANDOFF or RELEASE
-> FAILURE CLEANUP
```

Do not destructively clean up evidence or recovery state merely to make the workspace look finished.

## Autonomous continuation

Continue without asking "continue?" when all are true:

- the objective is clear;
- the exact next action is authorized;
- required capability/authority exists;
- the prior effect has been verified or reconciled;
- no true decision blocker has been reached.

Otherwise stop at the blocker instead of inventing work.
