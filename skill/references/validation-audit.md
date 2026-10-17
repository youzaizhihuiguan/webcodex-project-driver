# Validation, Integration, Evidence, and Audit

## Ownership boundary

The Project Driver owns **control-plane evidence semantics**:

- which exact Project/Session/Task/Attempt/Job/resource/result/candidate the evidence belongs to;
- whether the platform state was freshly re-observed;
- whether the evidence is current, terminal, failed, invalid, or uncertain;
- worker-result and integration-candidate provenance;
- stale fence/generation avoidance;
- result/artifact pullback and handoff;
- preservation of failed/invalid control-plane evidence.

Project-local instructions, domain Skills, and `agent-operating-model` own domain methods, acceptance thresholds, generic diagnosis/verification discipline, and whether independent review is required.

## Platform verification

After a stateful WebCodex effect, use the cheapest authoritative observation that establishes what happened.

Examples:

- exact Task/Attempt state;
- same Job identity reaching a terminal state;
- fresh Browser/Computer observation after structural change;
- artifact existence/content identity after transfer;
- live provider/capability state;
- project/domain evidence tied to the exact candidate/run.

"Command dispatched" is not proof that the intended higher-level validation passed.

## Worker evidence

When workers are used, retain enough to identify:

- exact assignment/Task/Attempt;
- predecessor/input/candidate identity;
- output/result/artifact identity;
- evidence location;
- unresolved platform risk/blocker;
- what was not verified.

A worker saying "done" is not itself completion evidence.

## Integration semantics

When multiple outputs converge:

1. identify one exact integration candidate;
2. verify required worker outputs are current and belong to compatible predecessors;
3. preserve conflict/dependency resolution provenance;
4. attach integration-level evidence to that exact candidate.

Several individually successful workers do not prove the integrated candidate.

Whether an Integrator is needed is an outer topology decision; this section only defines provenance once integration exists.

## Independent audit

Independent control-plane audit is **conditional**. Use it only when the user/project/operating model requires independence or a concrete material risk justifies it.

When used, a read-only auditor may verify:

- correct candidate/run identity;
- evidence provenance;
- stale-fence/generation avoidance;
- integration completeness;
- resource lifecycle/handoff;
- no fabricated provider/capability/wake path;
- no hidden replacement dispatch after uncertainty.

Domain correctness remains owned elsewhere.

## Evidence traceability

For material work, preserve enough provenance to explain an acceptance claim from exact durable objects:

~~~text
Task/assignment
-> Attempt/Session/Job
-> output/candidate/artifact
-> control-plane observation/evidence
-> integration candidate (if any)
-> audit verdict (if required)
~~~

This does not require a graph database or a standalone evidence artifact.

## Failure preservation

A failed formal WebCodex run remains failed historical evidence after remediation.

Do not overwrite the old run, hide an outcome-unknown effect behind replacement success, or relabel stale/invalid evidence as current.

A materially changed candidate/runtime protocol gets new evidence.

## Platform failure classification

Generic diagnosis belongs to the outer operating model/domain. For routing inside WebCodex, distinguish at least:

- stale identity/freshness;
- unavailable provider/capability/Host path;
- Runner/resource failure;
- transport/hosting/network uncertainty;
- Task/Attempt/Wait lifecycle error;
- integration/predecessor mismatch;
- artifact transfer/provenance mismatch;
- project/domain failure owned outside WebCodex.

Use [autonomy-escalation.md](autonomy-escalation.md) for the platform recovery path.

## Evidence versus delivery

Terminal backend state is not the same as user-visible result delivery.

When delivery matters, verify both the source terminal/result state and the substantive result/artifact pullback.
