# Long-Running Work

## Choose by lifecycle and ownership, not duration alone

### Ordinary process that becomes long

Start with the normal execution/validation path. If WebCodex hands the execution off as a Runner-owned Job, retain and observe that same Job identity.

### Intentionally asynchronous from the start

Use the runtime's asynchronous Job path when background execution is intentional and the Runner-owned lifecycle is appropriate.

### Must survive Runner restart/replacement

Use detached/supervisor-owned execution only when restart survivability actually requires it. Duration alone does not justify detachment.

### Persistent shell or remote resource

Use a persistent Session shell/SSH resource only when retaining remote shell state, environment, or interactive context is useful. Do not create one merely because several one-shot commands are needed.

### Durable delegated work

When a durable AgentTask/Attempt owns long work, keep Task/Attempt freshness separate from the execution backend's own Job/CodingAgentRun identity. Heartbeat or renew only according to the live contract; never assume ordinary polling or Agent presence extends an Attempt lease.

When the controller only needs terminal attention, prefer a supported AgentWait/Job-wait/Endpoint-Wake path over keeping one model turn open. See [event-driven-continuation.md](event-driven-continuation.md).

## Durable state for long work

For costly or formal long work, persist enough to recover:

- objective and phase;
- exact Task/Attempt/Job/process/shell/resource identity as applicable;
- execution backend identity when Task ownership and execution are separate;
- launch/start evidence;
- owner/supervisor and Runner placement;
- relevant configuration or input identity;
- Wait/Wake/continuation identity when terminal attention is armed;
- last observation and terminal/failure reason when known;
- evidence/result location;
- exact next action;
- whether replacement dispatch is forbidden until reconciliation.

Add Git SHA/ref, experiment config/hash, database namespace, research metadata, or other domain fields only when that domain needs them. See [durable-run-state.md](durable-run-state.md).

## Do not poll through one giant model turn

Prefer:

- start or reuse the exact Job/process;
- persist enough identity for recovery;
- establish supported attention/continuation only when live Host capability is verified;
- yield;
- later observe the same identity.

## Formal windows

For formal soak/burn-in/acceptance work:

- follow the project/domain protocol for fresh state and admission;
- preserve failed or invalid windows as historical evidence;
- do not silently change cadence, source scope, threshold, denominator, or retry semantics to make a run pass;
- create a new validation window after a material candidate/protocol change rather than relabeling old evidence.
