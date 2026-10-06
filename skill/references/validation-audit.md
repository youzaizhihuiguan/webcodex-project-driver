# Validation, Evidence, and Audit

## Ownership boundary

The Project Driver owns control-plane evidence semantics:

- which exact run/task/job/resource/result the evidence belongs to;
- whether evidence is current, terminal, failed, invalid, or uncertain;
- whether a state transition was actually re-observed;
- preservation of failed/invalid evidence;
- independent control-plane review at important gates;
- result pullback and handoff.

Domain Skills and project-local contracts own domain validation methods, thresholds, scientific criteria, test strategy, business acceptance, and other domain-quality judgments.

Do not duplicate those methods here.

## Verification

After a stateful action, use the cheapest authoritative observation that can establish what actually happened.

Examples:

- exact Task/Attempt terminal state;
- same Job identity reaching a terminal state;
- fresh Browser snapshot after navigation;
- artifact existence/content identity after transfer;
- project/domain validation evidence tied to the exact candidate/run.

"Command ran" is not the same as "the intended validation passed."

## Independent review

At major gates, use an independent read-only review/audit context when the project/domain risk justifies it.

The reviewer should verify control-plane facts such as:

- correct identity and candidate/run selection;
- evidence provenance;
- stale-fence/generation avoidance;
- failure containment;
- resource lifecycle/handoff;
- acceptance-state bookkeeping;
- no fabricated capability or hidden retry.

Domain correctness remains owned by the appropriate project/domain methodology.

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

- domain/product correctness;
- parser/schema/data contract;
- source/hosting;
- network/transport;
- third-party runtime/dependency;
- test/experiment contamination;
- Runner/control plane;
- acceptance/admission logic;
- missing capability or authority.

Fix the correct layer rather than treating every failure as an implementation bug.

## Evidence versus delivery

"Task resolved" is not the same as "result delivered to the user."

When completion matters, verify both terminal state and substantive result/artifact pullback.
