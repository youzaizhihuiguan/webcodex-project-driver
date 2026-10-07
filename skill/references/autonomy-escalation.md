# Autonomy and Escalation

## Principle

Automate execution mechanics aggressively inside a clear authorized contract. Escalate only when the next action changes objective, authority, risk acceptance, or irreversible external state.

## Automatic control actions

Usually continue without asking for confirmation when policy already authorizes the class of action:

- observe/reconcile exact existing state;
- read/search/analyze project material;
- execute bounded implementation assigned by the current objective;
- run focused validation;
- preserve evidence;
- perform safe remediation that does not change frozen acceptance semantics;
- coordinate exact Sessions/Tasks/Jobs;
- wait for already-started work;
- use a verified optional capability or safe fallback;
- checkpoint/handoff recovery state.

## Failure routing

### Uncertain outcome

Reconcile the same identity before retry.

### Stale selector/generation/revision

Acquire fresh state. Do not force the stale effect.

### Validation failure

Preserve FAIL evidence, classify the failure, make a bounded remediation when the fix is inside the authorized design, then create new evidence.

### Provider/capability unavailable

Use a verified fallback that preserves the objective, or stop at a capability blocker if no equivalent path exists.

### Runner/resource failure

Reconcile survival/ownership first, then recover from a durable checkpoint/artifact or make a new placement decision.

### Integration conflict

Do not let individual workers overwrite each other. Resolve in the integration stage against an explicit candidate/predecessor.

### Repeated failure

Do not loop indefinitely. Respect project-defined retry/cost/time budgets when present; otherwise stop when continued retries would no longer be evidence-driven.

## Human/project decision boundaries

Escalate when the next step requires:

- defining a missing objective;
- changing frozen architecture/scope/acceptance semantics;
- accepting a material unresolved risk;
- destructive cleanup/history rewrite;
- changing protected/default-branch or release state when not already authorized;
- installing/configuring a new privileged provider/runtime integration when that exceeds current authority;
- irreversible external action;
- exceeding an explicit cost/time/resource budget.

## Release boundary

Implementation readiness and release authority are separate.

A controller may prepare a verified release candidate while still stopping before merge/tag/publish/deploy if project policy reserves those effects.

## Reporting blockers

Report:

- exact blocked objective/phase;
- last verified state;
- relevant exact identities/evidence;
- why automatic fallback is insufficient;
- the smallest decision needed from the user/project owner;
- what will continue after that decision.

Do not ask "continue?" when no real decision exists.
