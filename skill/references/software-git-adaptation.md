# Software / Git Adaptation

Use this reference only when Git is an authoritative substrate and WebCodex must map project work onto checkouts or managed worktrees.

Generic branch/commit/push/review/release policy belongs to the repository/project and, when active, `agent-operating-model`. This reference owns **WebCodex checkout/worktree identity, selection, reuse, recovery, and cleanup mechanics**.

## Resolve current Git/workspace identity

Before a WebCodex-managed checkout/worktree mutation, resolve:

- exact repository and Project;
- checkout/worktree path;
- branch/ref/HEAD when applicable;
- actual workspace status;
- current WebCodex owner/Job/Task dependencies;
- whether another checkout/worktree already satisfies the required isolation.

Do not infer Git/workspace truth from chat memory.

## Selection policy

**Default to an existing suitable checkout.**

Create a new WebCodex-managed worktree only when a concrete requirement justifies filesystem isolation, such as:

- concurrent mutable branches/tasks that would otherwise conflict;
- preserving a stable checkout while another mutable candidate is developed;
- preserving a failed/experimental workspace that must remain inspectable;
- a genuinely independent audit/validation run whose filesystem isolation is material.

The labels **substantial**, **review**, and **long-running** are not sufficient reasons by themselves.

## Safe reuse

Before creating another managed worktree, inspect existing WebCodex Projects/worktrees for a compatible candidate.

Reuse an existing one only after verifying:

- same repository identity;
- suitable branch/ref/candidate;
- workspace state is understood;
- no conflicting active Task/Job/controller owns it;
- reuse will not destroy unique failed/experimental evidence;
- project policy permits that workspace to be reused.

Do not silently retarget a dirty or actively owned worktree.

## Build-output amplification

Treat Git worktree count and generated-output footprint as separate concerns.

Phase A measurement for this installation showed that the large managed-worktree footprint was dominated by replicated Rust `target/` build output, not Git worktree metadata itself. Therefore:

- do not solve disk pressure by discussing Git metadata alone;
- do not create a fresh worktree merely to obtain a clean build directory;
- inspect `target/`, `node_modules/`, virtual environments, caches, build/dist/out trees, and other generated state when capacity matters;
- use repository/toolchain-defined shared cache or output policies only when the owning project explicitly supports them;
- never invent a cross-worktree shared build/cache layout that could compromise correctness.

Capacity thresholds are review signals, not deletion authority.

## Recovery

After interruption, recover the exact Project/worktree plus:

- branch/ref/HEAD;
- actual status;
- active Task/Job ownership;
- relevant validation/evidence;
- only the unresolved workspace delta.

If a prior worktree create/remove/retarget operation has uncertain outcome, reconcile the WebCodex/Git state before retrying.

## Terminal cleanup

Remove a managed worktree only after all of the following are reconciled:

1. no active Task/Job/controller still owns or depends on it;
2. no unique uncommitted files remain;
3. important commits/candidates have durable refs according to project policy;
4. required evidence/artifacts have been promoted or preserved;
5. retained failure/experimental state is no longer required;
6. the outer project/authority contract permits cleanup.

Then:

- use Git/WebCodex-aware worktree removal rather than blind filesystem deletion;
- prune stale Git metadata when appropriate;
- reconcile WebCodex Project/registry state separately from the filesystem;
- decide branch/ref deletion separately from worktree removal;
- verify the expected disk/state change after cleanup.

A filesystem directory that is not represented by a matching WebCodex Project is a **reconciliation finding**, not an automatic deletion target.

## Generic Git policy boundary

This reference does not prescribe:

- when to create ordinary commits;
- whether to push;
- whether a PR or reviewer is required;
- protected/default-branch merge policy;
- release/tag policy.

Use the owning repository/user/platform contract for those decisions.
