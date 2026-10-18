# Software / Git Adaptation

Use this reference only when Git is authoritative and WebCodex must map work onto checkouts or managed worktrees.

Generic branch/commit/push/review/release policy belongs to the repository/project and, when active, `agent-operating-model`. This reference owns **WebCodex checkout/worktree admission, identity, provenance, reuse, recovery, generated-output interaction, and cleanup mechanics**.

## Contents

- [Resolve current Git/workspace identity](#resolve-current-gitworkspace-identity)
- [Worktree admission](#worktree-admission)
- [Read-only review rule](#read-only-review-rule)
- [Creation provenance](#creation-provenance)
- [Safe reuse](#safe-reuse)
- [Generated-output lifecycle](#generated-output-lifecycle)
- [Recovery](#recovery)
- [Terminal finalization](#terminal-finalization)
- [Unknown and legacy worktrees](#unknown-and-legacy-worktrees)
- [Generic Git policy boundary](#generic-git-policy-boundary)

## Resolve current Git/workspace identity

Before a WebCodex-managed checkout/worktree mutation, resolve:

- exact repository and Project;
- primary checkout and current managed worktrees;
- exact path, branch/ref/HEAD, and status;
- current WebCodex Task/Session/Job/controller ownership;
- existing worktree provenance/manifest when WebCodex created it;
- whether another checkout/worktree already satisfies the required isolation;
- known terminal/`cleanup_pending` worktree leases from earlier tasks.

Do not infer Git/workspace truth from chat memory.

## Worktree admission

**Default to an existing suitable checkout.**

A new managed worktree requires a concrete filesystem-isolation benefit, such as:

- concurrent mutable branches/tasks that would otherwise conflict;
- preserving a stable checkout while another mutable candidate is developed;
- preserving unique failed/experimental state that must remain inspectable;
- an audit/validation whose correctness materially depends on independent filesystem state.

The labels **substantial**, **review**, **fresh reviewer**, **independent**, or **long-running** are not sufficient reasons.

Before allocating a new worktree:

1. reconcile compatible existing worktrees and terminal leftovers;
2. determine why the current checkout or an existing worktree cannot safely serve;
3. determine expected path, owner, branch/candidate, lifetime, and whether heavy build output is expected;
4. verify current user/project/harness authority to create it.

If the current user/project has not already authorized that worktree class/allocation, present the reason, intended path/lifetime, and cleanup behavior before creation and obtain the required decision. Do not treat writable filesystem access as implicit worktree authority.

When creation is authorized, prefer the current WebCodex/harness-native managed-worktree primitive over ad-hoc shell construction.

## Read-only review rule

A fresh reasoning context does not require a fresh filesystem.

For immutable/read-only review, prefer in order:

1. inspect the immutable commit/candidate directly from an existing suitable checkout;
2. reuse an existing compatible read-only/review worktree when filesystem materialization is needed;
3. create a new worktree only if review correctness materially requires separate filesystem state.

Do not create one worktree per reviewer merely to make the reviewer "fresh".

## Creation provenance

Every WebCodex-created managed worktree must have recoverable creation provenance. Record enough in the owning resource/task manifest to establish:

- repository identity;
- exact worktree path;
- created-by-WebCodex provenance;
- owner Project plus strongest available Task/Session/Job/run;
- branch/ref/HEAD/base as relevant;
- purpose/isolation reason;
- creation time;
- retention class;
- cleanup condition/finalizers.

Cleanup consumes this provenance. Do not reconstruct ownership later from directory names alone.

## Safe reuse

Before creating another managed worktree, inspect existing WebCodex Projects/worktrees for a compatible candidate.

Reuse only after verifying:

- same repository identity;
- suitable branch/ref/candidate;
- workspace state is understood;
- no conflicting active owner exists;
- reuse will not destroy unique failed/experimental evidence;
- project policy permits reuse.

Do not silently retarget a dirty, locked, outcome-unknown, or actively owned worktree.

## Generated-output lifecycle

Worktree lifecycle and generated-output lifecycle are independent.

Heavy generated state such as `target/`, dependency trees, virtual environments, build/dist/out directories, caches, transport bundles, and copied validation artifacts must not be retained merely because the worktree remains.

When the toolchain/project permits a documented task-specific output location, prefer routing ephemeral build output to the owning task scratch. Otherwise track generated output in the worktree as owned regenerable state and finalize it separately.

Do not create a new worktree merely to obtain a clean build directory. Do not invent a shared cross-worktree cache/output layout that could compromise correctness.

> keep worktree != keep generated output

## Recovery

After interruption, recover the exact Project/worktree plus:

- creation provenance;
- branch/ref/HEAD and actual status;
- active Task/Job ownership;
- relevant validation/evidence;
- generated-output/resource state when material;
- cleanup state/finalizers;
- only the unresolved workspace delta.

If create/remove/retarget outcome is uncertain, reconcile the exact Git/WebCodex identity before retrying.

## Terminal finalization

A worktree owner reaching PASS/FAIL/SUPERSEDED/CANCELLED does not automatically make the filesystem safe to remove.

Before removing a WebCodex-owned managed worktree, reconcile these finalizers:

1. no active Task/Job/controller/process still owns or depends on it;
2. no unique uncommitted/untracked state remains;
3. important commits/candidates have durable refs according to project policy;
4. required evidence/artifacts have been promoted;
5. retained failed/experimental recovery state is no longer required;
6. current authority permits cleanup.

Then:

- finalize unneeded generated output independently;
- use Git/WebCodex-aware worktree removal rather than blind filesystem deletion;
- prune stale Git metadata when appropriate;
- reconcile/unregister the matching temporary WebCodex Project separately;
- decide branch/ref deletion separately from worktree removal;
- verify path, Git worktree list, registry, and expected disk change;
- mark the resource closed.

If a finalizer fails, keep the exact worktree/resource `cleanup_pending`; do not force-remove it merely to make closeout look clean.

Before another heavy worktree allocation for the same Project, reconcile known terminal/`cleanup_pending` owned worktrees first.

## Unknown and legacy worktrees

A filesystem directory or Git worktree without matching creation provenance is a reconciliation finding, not an automatic deletion target.

For unknown/foreign/legacy candidates:

- inspect status, refs, locks, activity/ownership, and unique state;
- classify/report before destructive action;
- never use broad `rm -rf` as a substitute for Git-aware removal;
- do not let a missing manifest trigger broad discovery deletion.

Broad scanning may find cleanup candidates, but only exact proven ownership or an explicit user decision authorizes removal.

## Generic Git policy boundary

This reference does not prescribe:

- when to create ordinary commits;
- whether to push;
- whether a PR/reviewer is required;
- protected/default-branch merge policy;
- release/tag policy.

Use the owning repository/user/platform contract for those decisions.
