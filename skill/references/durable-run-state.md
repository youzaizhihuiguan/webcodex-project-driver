# Durable Run State

## Scope

The outer user/project contract or `agent-operating-model` decides **whether** durable recovery state is needed and owns generic objective/scope/next-action semantics.

This reference defines the **WebCodex-specific fields** that make such a handoff recoverable without chat memory.

Do not force one storage mechanism. These fields may live in Goal/Session state, project files, a run directory, database state, Git metadata, or another project-owned store.

## Exact identities

Persist only identities that materially affect recovery, for example:

- Project and Runner;
- Workflow Session;
- Goal;
- Agent / Endpoint generation;
- AgentTask / Attempt;
- AgentWait / Wake;
- CodingAgentRun;
- Job/process;
- Browser/page;
- Computer surface/window;
- SSH resource / persistent shell;
- artifact or cross-Project transfer identity.

Do not collapse distinct runtime objects into one generic task id.

## Freshness selectors

Record or reference fences, generations, snapshots, observation tokens, replay/idempotency selectors, and file revisions only when a later continuation may safely reuse them.

Treat them as invalid when their owning snapshot/generation changes.

## Last verified platform state

Persist concise mechanical facts that a later controller can trust, such as:

- exact Job terminal/running state observed;
- exact Task/Attempt reconciled;
- current Runner/provider readiness;
- fresh Browser/Computer observation acquired after a structural change;
- delegated result body pulled back;
- artifact transfer hash verified;
- exact integration candidate identified.

Do not replace these facts with a worker's summary claim.

## Evidence and results

When material:

- result/artifact location and exact source identity;
- control-plane evidence provenance;
- PASS/FAIL/INVALID/UNKNOWN state when the outer validation contract uses it;
- retained failed evidence identity;
- integration candidate and included worker results;
- audit identity/verdict only when audit is actually required.

Domain methods and thresholds remain owned elsewhere.

## Resources and scratch

For important resources, persist:

- resource identity and owner;
- Runner/location;
- borrowed/owned and persistent/ephemeral state;
- release/handoff expectation;
- scratch Project/task path when recoverable temporary files exist;
- cleanup/promotion state.

Scratch is Runner-local and must not silently become authoritative project state.

## Wait / continuation state

When waiting or Host re-entry matters, persist:

- exact AgentWait/Job-wait/Wake identity;
- source Task/Job identities;
- any/all semantics when relevant;
- Agent/Endpoint generation;
- whether production Host continuation readiness was actually observed;
- consumed/pending wake state when relevant.

Wake delivery does not replace source-state reconciliation.

## Placement

When placement matters, persist:

- chosen Runner/surface;
- Project/resource identity on that Runner;
- hard platform/capability/locality reason;
- fallback placement if one is already defined.

Do not recompute placement from convenience after interruption while the original durable identity remains valid.

## Orchestration state

For active multi-worker WebCodex topology, persist enough to recover:

- controller/Goal/topology revision if used;
- each required Task and current Attempt;
- dependencies;
- assignee/backend;
- expected result/evidence;
- integration destination;
- whether replacement dispatch is forbidden until reconciliation;
- exact integration candidate after fan-in.

## Attention state

When progress depends on regaining model or human attention, persist:

- source identity;
- event class and last verified state;
- whether platform continuation is possible;
- delivery/wake state when known.

The outer task contract owns the generic decision about whether the user must be interrupted.

## Sufficiency invariant

WebCodex-specific recovery state is sufficient only if a new controller can determine:

1. which exact runtime objects still matter;
2. which are running, waiting, terminal, failed, or outcome-unknown;
3. which effect must not be repeated before reconciliation;
4. which freshness selectors remain valid;
5. where results/evidence/resources live;
6. which Runner/surface owns the state;
7. which waits/topology dependencies remain;
8. what exact WebCodex observation/effect is safe next.

Generic objective, project policy, acceptance criteria, and broader next-action authority come from their owning project/instruction layer.
