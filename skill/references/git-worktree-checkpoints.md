# Git, Worktrees, and Checkpoints

## Managed worktrees

Prefer WebCodex-managed worktrees for substantial write tasks when:
- another workspace must remain stable;
- independent audit/review must coexist;
- a failed runtime/evidence branch must be preserved;
- parallel tasks need filesystem isolation.

A worktree is another checkout of the same repository, not another Git history.

## Baseline

Resolve a human-readable ref to an exact commit before relying on it. Record exact SHA in formal handoffs.

## Commit policy

Commit at a recovery-worthy boundary:
- bounded implementation complete;
- focused validation passed;
- exact diff reviewed.

Prefer exact-path/structured commits when available. Avoid indiscriminate staging.

Important checkpoints should be pushed to a review/checkpoint branch when losing the local worktree would cause significant rework.

## Commit quality

A checkpoint should be:
- bounded;
- validated;
- explainable;
- reversible;
- attributable to one objective.

If a WIP checkpoint is unavoidable, label it explicitly as unvalidated and never treat it as PASS.

## Default branch

Do not equate "push review branch" with "merge default branch". Default/protected branch promotion remains a separate decision when project policy requires explicit authorization.

## Cleanup

Before removing a worktree:
1. inspect status;
2. verify no unique uncommitted files;
3. verify important commits have durable refs;
4. verify evidence/artifacts are archived;
5. remove the worktree;
6. prune stale worktree metadata;
7. decide branch deletion separately.

Never use bulk filesystem deletion as a substitute for Git-aware cleanup.
