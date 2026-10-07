# Validation, Integration, Evidence, and Audit

## Ownership boundary

The Project Driver owns control-plane evidence semantics:

- which exact run/task/attempt/job/resource/result/candidate the evidence belongs to;
- whether evidence is current, terminal, failed, invalid, or uncertain;
- whether a state transition was actually re-observed;
- preservation of failed/invalid evidence;
- integration identity and worker-result provenance;
- independent control-plane review at important gates;
- result pullback and handoff.

Domain Skills and project-local contracts own domain validation methods, thresholds, scientific criteria, test strategy, business acceptance, and other domain-quality judgments.

Do not duplicate those methods here.

## Verification

After a stateful action, use the cheapest authoritative observation that can establish what actually happened.

Examples:

- exact Task/Attempt terminal state;
- same Job identity reaching a terminal state;
- fresh Browser/Computer observation after structural change;
- artifact existence/content identity after transfer;
- project/domain validation evidence tied to the exact candidate/run.

"Command ran" is not the same as "the intended validation passed."

## Worker evidence

A worker result should identify:

- exact assignment/task;
- candidate/input identity;
- output/result/artifact identity;
- evidence produced;
- unresolved risk/blocker;
- what the worker did not verify.

A worker claiming "done" is not itself completion evidence.

## Integration gate

When multiple worker outputs converge, establish one exact integration candidate before final audit.

The Integrator may mutate only under explicit integration authority.

Integration should verify:

- required worker outputs are present and current;
- incompatible predecessors/generations are rejected;
- conflicts/dependencies are resolved;
- the combined candidate is identified exactly;
- integration-level validation is attached to that candidate.

Do not treat several individually passing workers as proof that the combined system passes.

## Independent audit

At major gates, use an independent read-only review/audit context when project/domain risk justifies it.

The reviewer should verify control-plane facts such as:

- correct candidate/run selection;
- evidence provenance;
- stale-fence/generation avoidance;
- integration completeness;
- failure containment;
- resource lifecycle/handoff;
- acceptance-state bookkeeping;
- no fabricated capability/provider/wake path;
- no hidden retry or replacement dispatch after uncertainty.

Domain correctness remains owned by the appropriate project/domain methodology.

## Evidence graph

For important work, maintain enough provenance to trace:

~~~text
objective/requirement
-> Task/assignment
-> Attempt/Session/Job
-> output/candidate/artifact
-> validation evidence
-> integration candidate
-> audit verdict
~~~

Not every project needs a literal graph database. The invariant is traceability: an acceptance claim should be explainable from exact durable identities and evidence.

## Failure preservation

A failed formal run remains failed historical evidence even after a fix.

Do not:

- overwrite old evidence;
- resume an invalidated formal window as if it were clean;
- hide a primary failure behind retry success;
- lower frozen thresholds/denominators merely to pass;
- cross-mask one failure source/class with another.

A materially changed candidate or protocol gets new evidence.

## Failure classification

Before remediation, identify the failing layer sufficiently to choose the right owner, for example:

- objective/authority;
- domain/product correctness;
- integration conflict;
- parser/schema/data contract;
- source/hosting/network/transport;
- third-party runtime/dependency;
- test/experiment contamination;
- Runner/control plane;
- stale identity/freshness;
- unavailable provider/capability;
- acceptance/admission logic.

Fix the correct layer rather than treating every failure as an implementation bug.

Use [autonomy-escalation.md](autonomy-escalation.md) to decide whether remediation can continue automatically.

## Evidence versus delivery

"Task resolved" is not the same as "result delivered to the user."

When completion matters, verify both terminal state and substantive result/artifact pullback.
