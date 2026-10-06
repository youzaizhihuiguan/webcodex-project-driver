# Validation and Audit

## Layer validation

Use the cheapest evidence that can falsify the current change first.

Typical order:
1. static/lint/type checks relevant to the change;
2. focused regression tests;
3. affected integration/database tests;
4. independent review/audit;
5. full or formal validation at a phase gate.

Do not run the entire project test/audit suite after every tiny change unless the project requires it.

## Audit separation

At major gates, prefer an independent read-only review context that did not implement the change.

Audit:
- code correctness;
- acceptance/control logic;
- denominator/accounting;
- failure containment;
- lifecycle cleanup;
- evidence integrity;
- docs/config drift;
- runtime restart/overlap behavior where relevant.

## Failure preservation

A failed formal run remains failed historical evidence even after a code fix.

A new candidate gets a new validation window.

Do not:
- overwrite old evidence;
- resume an invalid formal run;
- hide a primary failure behind retry success;
- cross-mask one source/class with another;
- lower a frozen threshold merely to pass.

## Failure classification

Before remediation, distinguish:
- product correctness defect;
- parser/schema defect;
- source/hosting behavior;
- network/transport issue;
- third-party runtime/dependency behavior;
- test contamination;
- runner/control-plane defect;
- acceptance/admission defect.

Fix the correct layer.

## Evidence versus assertion

"Tests ran" is not the same as "the intended tests ran".
"Hash recorded" is not the same as "hash compared and enforced".
"Task resolved" is not the same as "result delivered to the user".

Prefer mechanical evidence.
