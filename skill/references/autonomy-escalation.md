# WebCodex Failure Routing and Escalation

## Scope

Generic scope control, approval gates, material-mutation authority, and proportional rigor belong to the user/project contract and, when active, `agent-operating-model`.

This reference only describes how WebCodex-specific failure states should be reconciled and what platform facts must be surfaced when automatic continuation is impossible.

## Platform failure routing

### Uncertain outcome

Reconcile the same exact Session/Task/Attempt/Job/resource/action identity before retry or replacement dispatch.

### Stale selector / generation / snapshot / revision

Acquire fresh state from the owning runtime object. Do not force an effect through stale proof.

### Provider or capability unavailable

Verify current Runner/provider/Host readiness. Use an equivalent verified WebCodex path if the outer task contract permits it; otherwise surface the missing capability as a platform blocker.

### Runner or resource failure

Reconcile survival, ownership, and last durable state first. Recover from an exact checkpoint/artifact or make a new placement decision only after duplicate/corruption risk is resolved.

### Wait / wake / Host continuation unavailable

Keep exact source identities and last verified state. Downgrade to later-turn recovery instead of pretending auto-resume exists.

### Integration conflict

Keep worker outputs tied to exact predecessors/candidates. Resolve the conflict at an explicit integration candidate rather than allowing workers to overwrite one another.

### Repeated platform failure

Do not loop on the same WebCodex operation without new evidence. Preserve the last verified state and expose the platform limitation/failure to the outer task controller.

## Attention routing

Use [attention-routing.md](attention-routing.md) to keep durable event truth separate from user/Host delivery.

This Skill does not decide that every failure needs human approval. The outer project/operating model decides whether a real user decision exists; this Skill provides the exact WebCodex state needed for that decision.

## WebCodex-specific blockers

Examples include:

- exact Project/Runner/Session/Task/Job/resource identity cannot be resolved safely;
- required freshness/fence/generation cannot be refreshed;
- prior effect remains outcome-unknown and duplicate execution would be unsafe;
- required provider/capability/Host path is unavailable with no permitted equivalent;
- Runner/resource ownership is unresolved;
- a cross-Project/artifact transfer cannot establish source/destination provenance.

When blocked, report the exact affected identity, last verified platform state, why a verified fallback is unavailable, and the smallest platform fact/authority needed to continue.

Do not manufacture a generic approval or review gate merely because the runtime exposes one.
