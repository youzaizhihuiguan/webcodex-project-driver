# Durable Run State

## Purpose

Persist enough state that a new controller can safely continue substantial WebCodex work without relying on chat memory.

Do not force one storage mechanism. Durable state may live in WebCodex Goal/Session state, project files, a run directory, a database row, Git metadata, or another project-owned store.

## Minimum recoverable fields

Persist these when they materially affect recovery.

### Objective

- exact current objective;
- scope/constraints that limit allowed work.

If the objective is missing or ambiguous, record that as a blocker instead of inventing work.

### Phase / status

- current phase;
- lifecycle state such as planned / active / blocked / waiting / failed / complete / abandoned;
- phase revision/generation when the project/domain uses one.

### Active identities

Record only relevant exact identities, for example:

- Project and Runner;
- Workflow Session;
- durable Goal;
- durable Agent / Endpoint generation;
- AgentTask / Attempt;
- AgentWait / Wake;
- CodingAgentRun;
- Job/process;
- Browser/page;
- Computer surface/window;
- SSH resource / persistent shell;
- artifact or domain-run identity.

Do not collapse these into one generic "task id."

### Freshness selectors

Store or reference fences/generations/snapshots/observation tokens/replay selectors only when a later continuation is allowed to reuse them.

Treat ephemeral selectors as invalid after their owning snapshot/generation changes.

### Evidence and results

- evidence/result locations;
- provenance;
- formal PASS/FAIL/INVALID/UNKNOWN where applicable;
- immutable failed evidence references;
- substantive delegated result/artifact locations.

### Resources

For important resources:

- identity;
- owner;
- Runner/location;
- borrowed/owned;
- persistent/ephemeral;
- expected release/handoff behavior;
- cleanup status.

### Last verified state

Write a concise mechanical statement of what is actually known true.

Examples:

- exact Job terminal state observed;
- exact AgentTask Attempt reconciled terminal;
- fresh Browser snapshot acquired after navigation;
- delegated Session result body pulled back;
- artifact transfer SHA verified;
- Git HEAD/status verified in a software adaptation.

### Exact next action

Prefer one mechanically actionable continuation step.

Good:

- observe exact Job X; do not redispatch;
- reconcile exact CodingAgentRun R bound to Attempt A;
- resume Session Y and inspect unresolved assignment Z;
- acquire a fresh Browser snapshot before the next element action;
- wait for exact Tasks A/B/C, then integrate candidate K;
- run the Windows validation leg against candidate C.

Avoid vague handoffs such as "continue testing" or "finish the work."

### Decision blockers

Record only real gates:

- missing objective;
- user approval;
- missing authority;
- missing capability/provider;
- no suitable Runner/placement;
- frozen-contract change;
- risk acceptance;
- destructive cleanup;
- protected/default-branch promotion or release;
- irreversible external action.

## Orchestration extensions

When multi-Agent/multi-Runner work exists, also persist enough to recover:

### Controller

- controller Agent/Session identity when used;
- Goal identity/revision;
- current topology revision.

### Task graph

For each required work unit:

- Task identity;
- assignee;
- current Attempt identity/state;
- dependencies;
- expected result/evidence;
- integration destination;
- whether replacement dispatch is forbidden until reconciliation.

### Wait / continuation state

- exact AgentWait or Job wait identity;
- source identities;
- mode (any/all) when relevant;
- Endpoint/controller generation;
- whether production auto-resume/readiness was actually observed;
- consumed/pending Wake state when relevant.

### Placement

- chosen Runner/surface;
- placement reason;
- capability/platform requirement;
- project/data locality;
- fallback placement if defined.

Do not recompute placement from scratch after interruption if the original resource identity still exists and remains valid.

### Integration / audit

- exact integration candidate identity;
- worker results included/excluded;
- integration validation state;
- independent audit identity/verdict;
- remediation delta if blocked.

## Sufficiency invariant

Durable run state is sufficient only if a new controller can determine:

1. what objective is authorized;
2. what is already done;
3. what is still running, waiting, blocked, or uncertain;
4. what must not be repeated;
5. what evidence/results exist;
6. what resources/Runners are involved;
7. what topology/dependencies remain;
8. what exact action is safe next;
9. what decision, if any, blocks continuation.
