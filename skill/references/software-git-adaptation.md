# Software / Git Adaptation

Use this reference only when Git is an authoritative substrate for the target software project. Git/worktree/checkpoint semantics are not universal WebCodex truths.

## Baseline

Before mutation, resolve the relevant human-readable ref to an exact commit and inspect the actual workspace state.

Do not infer repository truth from chat memory.

## Managed worktrees

Prefer a WebCodex-managed worktree for substantial write/review work when:

- another checkout must remain stable;
- independent audit/review must coexist;
- failed runtime/evidence state must be preserved;
- parallel tasks need filesystem isolation.

A worktree is another checkout of the same repository, not a separate Git history.

## Commit/checkpoint policy

Create a recovery-worthy checkpoint when a bounded software unit is complete enough to preserve.

A good checkpoint is:

- tied to one objective;
- exact about its predecessor;
- validated to the level required by the owning project/domain;
- reviewed for the intended diff;
- reversible/explainable.

If a WIP checkpoint is necessary for durability, label its validation state explicitly. Never treat an unvalidated commit as PASS.

## Push policy

Push an important review/checkpoint branch when remote recovery materially reduces risk.

Do not equate:

- local commit;
- branch push;
- protected/default-branch merge.

They are separate actions with separate authority.

## Recovery

For interrupted Git work, recover:

1. exact Project/worktree;
2. exact branch/ref/HEAD;
3. actual status;
4. relevant validation/evidence;
5. known Job/Session state;
6. only the uncompleted delta.

This extends the generic recovery model; it does not replace it.

## Cleanup

Before removing a worktree or branch:

1. inspect status;
2. verify no unique uncommitted files;
3. verify important commits have durable refs;
4. preserve evidence/artifacts;
5. remove the worktree only when safe;
6. prune stale metadata if needed;
7. decide local/remote branch deletion separately.

Never use bulk filesystem deletion as a substitute for Git-aware cleanup.
