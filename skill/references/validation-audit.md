# Validation, Integration, Evidence, and Audit

## Ownership boundary

The Project Driver owns **control-plane evidence semantics**:

- which exact Project/Session/Task/Attempt/Job/resource/result/candidate the evidence belongs to;
- whether the platform state was freshly re-observed;
- whether the evidence is current, terminal, failed, invalid, or uncertain;
- worker-result and integration-candidate provenance;
- stale fence/generation avoidance;
- result/artifact pullback and handoff;
- staging/promotion/retention of WebCodex-created evidence material;
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

## Evidence staging and promotion

Treat WebCodex-created raw evidence as staged material until the owning project/validation contract requires it durably.

Raw/staged examples:

- complete logs;
- screenshots;
- benchmark/raw JSON;
- copied/extracted source trees;
- transport tar/zip bundles;
- dependency/build trees;
- temporary validation databases/state.

Prefer promoting compact durable evidence sufficient to reconstruct the acceptance claim, such as:

- exact candidate/ref/hash;
- exact Task/Attempt/Job identity;
- PASS/FAIL/INVALID state and test counts;
- required receipt/log excerpt;
- artifact hash/location;
- necessary screenshots.

Do not retain a complete build tree, dependency tree, transport archive, or extracted source copy merely because it participated in validation.

If a large binary/result must become durable and the project has no declared artifact location/retention policy, surface the proposed durable destination before persisting it.

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

A fresh reviewer does not imply a fresh worktree. Filesystem isolation is governed by [software-git-adaptation.md](software-git-adaptation.md).

Domain correctness remains owned elsewhere.

## Evidence staging and promotion

Raw validation material is not automatically durable evidence.

Keep temporary logs, screenshots, JSON, copied source, transfer archives, unpacked validation trees, dependency trees, and build output in the owning scratch/resource lease unless the project already declares them durable.

At acceptance/closeout:

1. identify the minimum durable evidence the project/domain contract actually needs;
2. promote that evidence to the project-owned artifact/evidence location;
3. record provenance/hash/identity linking it to the exact run/candidate;
4. leave reproducible intermediates classified as owned ephemeral/regenerable so lifecycle finalization can reclaim them.

Prefer compact, reconstructable evidence such as candidate SHA, Job/Task identity, verdict/test counts, receipt, artifact hash/location, required log excerpts, or necessary screenshots.

A build tree, dependency directory, source-transfer archive, or extracted repository copy is not formal evidence merely because it participated in validation.

If a large binary must become durable evidence and no destination/retention policy exists, surface that storage decision rather than persisting it in an arbitrary workspace.

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

This does not require a graph database, a standalone evidence bundle, or retention of reproducible intermediates.

## Failure preservation

A failed formal WebCodex run remains failed historical evidence after remediation.

Preserve the failed run's required provenance/result, but do not equate failure preservation with retaining every reproducible build/output directory or transport copy.

Do not overwrite the old run, hide an outcome-unknown effect behind replacement success, or relabel stale/invalid evidence as current.

A materially changed candidate/runtime protocol gets new evidence.

Failure preservation applies to the required durable failed-run provenance/result. Preserve raw workspace/build state only when the project contract or unresolved diagnosis/recovery actually needs it; otherwise promote the required evidence and finalize the ephemeral resource.

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

When delivery matters, verify both the source terminal/result state and the substantive result/artifact pullback. After required durable evidence is promoted, release unneeded staged evidence through the owning resource lifecycle rather than leaving it in project/source directories.
