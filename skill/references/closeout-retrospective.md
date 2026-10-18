# WebCodex Closeout and Retrospective

## Scope

The outer project or `agent-operating-model` decides when a phase/objective is substantively complete and what acceptance means.

This reference defines the WebCodex-specific **resource finalization** required after that substantive outcome. For WebCodex-owned ephemeral resources, finalization is not optional housekeeping.

## Completion model

Keep these facts separate:

~~~text
substantive result terminal
!=
result delivered
!=
resource lifecycle closed
~~~

An accepted/failed/superseded/cancelled Task, Job, Session, validation run, or phase may still have owned resources in `finalizing` or `cleanup_pending`.

Only mark the WebCodex-owned resource lifecycle closed after required results are promoted, finalizers are satisfied, owned ephemeral state is reclaimed, obsolete control-plane objects are retired, and the expected state/disk delta is verified.

## Control-plane closeout

For a safely terminal bounded unit:

1. reconcile every required Task/Attempt/Job/worker result;
2. verify the exact integration candidate when parallel outputs converged;
3. verify control-plane evidence belongs to that exact run/candidate;
4. pull back required delegated results/artifacts;
5. promote only required durable scratch/evidence/artifacts;
6. reconcile resource owners, retention classes, and cleanup finalizers;
7. reclaim owned ephemeral and unneeded regenerable state;
8. close obsolete Sessions and retire temporary Task/Wait/Endpoint state when recovery provenance remains reconstructable;
9. unregister temporary Projects whose filesystem/runtime role is finished;
10. reconcile pending Wait/Wake/attention state;
11. verify filesystem, Git/worktree, registry, Job/Session, and disk state affected by cleanup;
12. persist any remaining `cleanup_pending` blocker and exact next cleanup action.

For Git/worktree cleanup, use [software-git-adaptation.md](software-git-adaptation.md).

For Runner-local scratch/build/validation resources, use [scratch-lifecycle.md](scratch-lifecycle.md).

## Finalizers

Before destructive cleanup of a WebCodex-owned resource, reconcile only the finalizers relevant to that resource, such as:

- exact owner is terminal/reconciled;
- no active Task/Job/process/controller still depends on it;
- no outcome-unknown effect still needs the resource;
- required durable result/evidence has been promoted;
- no unique dirty/uncommitted/recovery state would be lost;
- current user/project/platform authority permits the effect;
- the path/resource identity still matches the recorded creation provenance.

If a finalizer is unresolved, do not force cleanup. Keep the exact resource `cleanup_pending` with the blocker recorded.

## Cascading owned-resource cleanup

When one WebCodex-owned execution unit created dependent resources, finalize them as one ownership bundle rather than hoping each layer remembers independently.

For example, a native validation run may own:

~~~text
temporary Project
Session
source transport archive
extracted source copy
build/dependency output
raw logs/evidence
result receipt
~~~

After the result receipt/evidence is promoted, reclaim the other owned ephemeral dependents and verify the bundle no longer leaks control-plane or disk state.

This is scoped cascading cleanup, not a broad filesystem GC.

## Generated-output closeout

Generated state is separately reclaimable even when the checkout/worktree remains authoritative.

At terminal closeout, inspect and remove unneeded owned regenerable state such as:

- Cargo/other build output;
- dependency trees installed only for the completed validation;
- dist/build/out directories;
- task-scoped caches;
- source/frontend tar/zip bundles;
- extracted validation copies.

Do not preserve these merely because the worktree, branch, or formal evidence remains.

## Pre-allocation recovery

Before allocating another heavy worktree/validation workspace/build for the same Project, reconcile known prior owned resources that are already terminal or `cleanup_pending`.

This catches interrupted closeout before disk growth compounds.

Do not turn this into broad discovery deletion: only exact known/manifested ownership or an explicit user decision authorizes cleanup.

## Unknown / foreign resources

If a directory/resource lacks reliable WebCodex ownership provenance, treat it as foreign/unknown.

Inspection may classify it and report reclaimable space, but automatic deletion is not authorized merely by age, name, apparent staleness, or location.

Unknown, dirty, unpushed, locked, active, or otherwise ambiguous state is protected until authority is resolved.

## Cleanup failure and retry

Cleanup should be idempotent/recoverable.

If some cleanup steps succeed and another fails:

- do not recreate already removed resources;
- do not discard the ownership/cleanup record;
- persist `cleanup_pending` plus the remaining exact delta;
- later resume the same cleanup from live state.

Resource lifecycle becomes `closed` only after required cleanup and verification succeed.

## Completion versus delivery

A control-plane object may be terminal while the substantive result has not yet been pulled back or surfaced.

Closeout is incomplete when result delivery/handoff is required but only backend status has been observed.

Likewise, result delivery does not prove owned resources were finalized.

## Retrospective

Promote only stable WebCodex-specific lessons, for example:

- missing ownership/provenance that made cleanup unsafe;
- a placement rule that allowed temporary state into user/project directories;
- a finalizer/cleanup state that impaired recovery;
- an identity/freshness rule that prevented duplicate work;
- a provider/Host readiness assumption that proved false;
- a Runner/resource ownership problem;
- a control-plane composition ambiguity.

Keep project-specific policy, generic workflow methodology, and domain lessons in their owning layers.
