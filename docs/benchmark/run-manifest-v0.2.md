# Draft: cross-domain run manifest for v0.2

Status: benchmark design only.

## Goal

Define the minimum durable state needed to resume a substantial WebCodex workflow without relying on chat memory.

The manifest is conceptual. It may be represented by:
- WebCodex Goal/Session state;
- project files;
- a research state file;
- a run directory;
- Git metadata;
- a database row;
- another project-owned durable store.

Do not force one storage format across every domain.

## Core fields

### 1. Run identity

- `run_id`
- `objective`
- `owner/controller` when relevant
- `created_at`
- `last_verified_at`

### 2. Current phase/state

- `status`: planned / active / blocked / waiting / failed / complete / abandoned
- `phase`
- `phase_revision` or equivalent if the domain uses one

### 3. Exact execution context

Record only what matters:
- WebCodex Project id(s);
- Workflow Session id(s);
- Goal id;
- AgentTask/Attempt ids;
- Job ids;
- Runner/client id;
- browser/page ids;
- SSH resource / persistent shell identity.

### 4. Freshness selectors

Store only when a later continuation is allowed to reuse them.

Examples:
- assignment fence;
- Attempt fence + controller generation;
- Job observation token/ref;
- Browser snapshot/ref state;
- continuation generation.

Selectors known to be ephemeral should not be treated as durable identity.

### 5. Active work

For each active unit:
- exact identity;
- current known lifecycle state;
- launch/start evidence;
- last observation;
- retry/replay key if applicable;
- whether replacement dispatch is forbidden until reconciliation.

### 6. Evidence

- validation/evidence locations;
- logs/artifacts;
- source/provenance;
- PASS/FAIL/INVALID where formal judgment exists;
- immutable failed evidence references.

### 7. Resources

For each resource:
- identity;
- owner;
- persistent/ephemeral;
- borrowed/owned;
- expected release/handoff behavior;
- cleanup status.

### 8. Last verified state

A concise mechanical summary of what is known true.

Examples:
- Job terminal PASS at observation token X;
- Browser navigation completed and new snapshot acquired;
- Git HEAD exact SHA and worktree clean;
- research phase 3 evidence recorded;
- Session todo resolved and answer content pulled back.

### 9. Exact next action

One mechanically actionable next step.

Avoid vague handoff text such as:
- "continue testing";
- "finish the work";
- "look at the other window".

Prefer:
- "resume Session wc_sess_X and read todo wc_msg_Y";
- "observe Job wc_job_Z; do not redispatch";
- "acquire a fresh browser snapshot for page P before the next click";
- "run phase 4 using evidence paths A/B/C".

### 10. Decision blockers

Record only real gates:
- user approval;
- missing authority;
- missing capability/provider;
- frozen-contract change;
- risk acceptance;
- destructive cleanup;
- protected/default-branch promotion.

## Domain extensions

### Software engineering

May add:
- repository;
- exact commit SHA;
- branch/ref;
- worktree;
- validation command/evidence;
- changed paths.

### Research

May add:
- question/hypothesis;
- source/evidence ledger;
- phase outputs;
- experiment metadata;
- assumptions/limits.

### Browser/computer

May add:
- current URL/app;
- page/surface identity;
- snapshot generation;
- borrowed user resource status;
- human-takeover state.

### Remote operations

May add:
- remote host/resource;
- shell identity;
- process/Job identity;
- restart survivability;
- environment/config hash.

## Invariant

A manifest is sufficient only if a new controller can determine:

1. what is already done;
2. what is still running;
3. what must not be repeated;
4. what evidence exists;
5. what exact action is safe next.
