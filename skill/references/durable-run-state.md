# Durable Run State

## Purpose

Persist enough state that a new controller can safely continue substantial WebCodex work without relying on chat memory.

Do not force one storage mechanism. The durable state may live in WebCodex Goal/Session state, project files, a run directory, a database row, Git metadata, a research state file, or another project-owned store.

## Minimum recoverable fields

Persist these when they materially affect recovery:

### Objective

- exact current objective;
- scope/constraints that limit allowed work.

If the objective is missing or ambiguous, record that as a blocker instead of inventing work.

### Phase / status

- current phase;
- lifecycle state such as planned / active / blocked / waiting / failed / complete / abandoned;
- phase revision/generation when the domain uses one.

### Active work identities

Record only relevant exact identities, for example:

- Project;
- Workflow Session;
- Goal;
- AgentTask / Attempt;
- Job;
- Browser/page;
- Computer surface;
- SSH resource / persistent shell;
- artifact or domain-run identity.

### Freshness selectors

Store or reference fences/generations/snapshots/observation tokens only when a later continuation is allowed to reuse them. Treat ephemeral selectors as invalid after their owning snapshot/generation changes.

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
- borrowed/owned;
- persistent/ephemeral;
- expected release/handoff behavior;
- cleanup status.

### Last verified state

Write a concise mechanical statement of what is actually known true.

Examples:

- exact Job terminal state observed;
- fresh Browser snapshot acquired after navigation;
- delegated Session result body pulled back;
- research phase evidence persisted;
- Git HEAD/status verified in a software adaptation.

### Exact next action

Prefer one mechanically actionable continuation step.

Good:

- observe exact Job X; do not redispatch;
- resume exact Session Y and inspect unresolved assignment Z;
- acquire a fresh Browser snapshot before the next element action;
- execute phase 4 using evidence A/B/C.

Avoid vague handoffs such as "continue testing" or "finish the work."

### Decision blockers

Record only real gates:

- missing objective;
- user approval;
- missing authority;
- missing capability/provider;
- frozen-contract change;
- risk acceptance;
- destructive cleanup;
- protected/default-branch promotion.

## Sufficiency invariant

Durable run state is sufficient only if a new controller can determine:

1. what is already done;
2. what is still running or uncertain;
3. what must not be repeated;
4. what evidence exists;
5. what resources remain owned/borrowed;
6. what exact action is safe next;
7. what decision, if any, blocks continuation.
