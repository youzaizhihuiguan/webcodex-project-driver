# Closeout and Retrospective

## Control-plane closeout

At a phase/stage closeout:

1. verify the intended objective/phase status;
2. verify required domain/project evidence exists and belongs to the exact run/candidate;
3. preserve failed/invalid formal evidence;
4. update durable run state and authoritative project status;
5. record accepted/deferred risks separately from strict PASS/FAIL;
6. surface substantive delegated results/artifacts;
7. hand off or release owned/borrowed resources according to policy;
8. close obsolete Sessions/Tasks/Jobs only when doing so cannot destroy needed recovery evidence;
9. leave an exact next action when more work remains.

For Git/worktree cleanup in software projects, use [software-git-adaptation.md](software-git-adaptation.md).

## Completion versus strict acceptance

Operational/engineering completion and strict domain acceptance may differ.

Do not relabel old FAIL evidence merely because the project chooses to proceed with an explicitly accepted risk.

## Resource cleanup

Before destructive cleanup, verify:

- ownership;
- persistence expectations;
- whether another worker/run still depends on the resource;
- whether unique evidence or uncommitted state remains;
- whether the project requires explicit authorization.

Failure cleanup should preserve recoverability first.

## Retrospective

Collect lessons about:

- which control rule prevented duplicate/stale work;
- what state should have been persisted earlier;
- which capability/runtime assumption was wrong;
- what caused unnecessary rediscovery;
- where domain ownership versus control-plane ownership was unclear.

Promote only stable WebCodex/control lessons into this Skill. Keep project-specific/domain methodology in the owning project or domain Skill.
