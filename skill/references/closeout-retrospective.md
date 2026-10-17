# WebCodex Closeout and Retrospective

## Scope

The outer project or `agent-operating-model` decides when a phase/objective needs durable closeout and what project acceptance means.

This reference defines the WebCodex-specific reconciliation and resource work that may be required at such a closeout.

## Control-plane closeout

When applicable:

1. reconcile every required Task/Attempt/Job/worker result;
2. verify the exact integration candidate when parallel outputs converged;
3. verify control-plane evidence belongs to that exact run/candidate;
4. reconcile independent audit only when the outer contract actually required it;
5. preserve failed/invalid platform evidence;
6. pull back required delegated results/artifacts;
7. hand off or release owned/borrowed resources and Runner placements;
8. promote required scratch evidence/artifacts, then clean terminal task scratch that no longer carries recovery value;
9. reconcile pending Wait/Wake/attention state;
10. retire obsolete Sessions/Tasks/Jobs/endpoints only when needed recovery provenance remains reconstructable;
11. persist the WebCodex-specific handoff fields required for later recovery.

For Git/worktree cleanup, use [software-git-adaptation.md](software-git-adaptation.md).

For Runner-local scratch, use [scratch-lifecycle.md](scratch-lifecycle.md).

## Resource cleanup

Before destructive WebCodex resource cleanup, reconcile:

- exact owner;
- persistence expectation;
- live Task/Job dependencies;
- unique evidence/uncommitted recovery state;
- outer authority for cleanup when required.

Prefer cleanup at the owned task/resource boundary after promotion/reconciliation rather than guessed bulk deletion.

For multi-worker work, do not destroy identities/resources while the accepted candidate's provenance still depends on them.

## Completion versus delivery

A control-plane object may be terminal while the substantive result has not yet been pulled back or surfaced.

Closeout is incomplete when result delivery/handoff is required but only backend status has been observed.

## Retrospective

Promote only stable WebCodex-specific lessons, for example:

- an identity/freshness rule that prevented duplicate work;
- a missing durable platform field that impaired recovery;
- a provider/Host readiness assumption that proved false;
- a Runner/resource ownership problem;
- a control-plane composition ambiguity.

Keep project-specific policy, generic workflow methodology, and domain lessons in their owning layers.
