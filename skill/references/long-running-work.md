# Long-Running Work

## Choose by lifecycle, not just duration

### Ordinary process that becomes long
Start with the normal execution/validation tool. If it hands off as a Job, keep observing that same Job.

### Intentionally asynchronous from the start
Use the runtime's immediate asynchronous Job path when background execution is intentional.

### Must survive Runner restart/replacement
Use detached/supervisor-owned native execution from the start. Duration alone does not justify detachment.

## Run manifest

For formal or costly long work, persist enough identity to recover:
- exact candidate commit;
- branch/ref;
- Job ID;
- start timestamp;
- config/manifest hashes;
- DB/namespace/watermark identity where relevant;
- acceptance window parameters;
- terminal/failure reason.

## Do not poll through one giant model turn

Prefer:
- start/reuse Job;
- establish durable attention/continuation if the Host supports it;
- yield;
- recover the same Job later.

## SSH / server operations

Use a persistent Session shell only when retaining remote shell state is useful. Register/bind named SSH resources according to the current runtime contract.

Do not create a persistent shell merely because several one-shot commands are needed.

## Formal windows

For formal soak/burn-in/acceptance work:
- use fresh runtime/history state when required by the protocol;
- never resume an invalidated formal window;
- preserve failed output;
- do not silently change cadence/threshold/denominator to make the run pass.
