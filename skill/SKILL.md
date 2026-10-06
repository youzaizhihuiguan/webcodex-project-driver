---
name: webcodex-project-driver
description: Drive substantial software-engineering projects through WebCodex with durable state, managed worktrees, Git checkpoints, short bounded execution batches, validation/audit gates, long-running Job recovery, explicit Session/Goal/Task identities, and interruption-safe handoffs. Use when ChatGPT is asked to implement, refactor, audit, debug, validate, operate, or continue a multi-step codebase project through WebCodex, especially when work may span multiple model turns, worktrees, branches, long-running processes, or independent audit/execution sessions.
---

# WebCodex Project Driver

Treat the project lifecycle as durable and the current model turn as disposable.

## Core rules

1. Establish real state before acting. Use WebCodex to inspect the actual Project, exact Session when known, Git HEAD/ref/status, relevant validation/evidence, and known Jobs. Do not reconstruct repository truth from chat memory.
2. Never use a browser tab/window as a task identity. Address exact Project, Session, Goal, AgentTask, Job, branch, and commit identities where they matter.
3. Keep model turns short and bounded. Continue the overall project autonomously when safe, but split work into recoverable batches instead of one giant turn.
4. For write work, isolate tasks with a WebCodex-managed worktree when parallelism, review, formal validation, or preservation of another workspace matters.
5. Turn completed, validated work into durable Git checkpoints. Push important review/checkpoint branches when remote recovery materially reduces risk.
6. Never redispatch a long-running operation merely because the chat/window was interrupted. Recover the exact Job/Task first.
7. Separate implementation from independent audit at major gates.
8. Preserve failed formal evidence. Do not lower thresholds, alter denominators, hide retries, or overwrite failed windows merely to obtain PASS.
9. Gate optional capabilities on observed runtime configuration. Tool existence does not prove a provider, LSP server, Host continuation, plugin, or remote resource is configured.
10. Return delegated results to the user. A resolved Session message or terminal Task is not sufficient if the result body was never surfaced.

## Decide the execution mode

For a trivial read or tiny edit, use the simplest direct WebCodex path.

For substantial work, use the project workflow in [references/execution-model.md](references/execution-model.md).

For write isolation and durable Git checkpoints, read [references/git-worktree-checkpoints.md](references/git-worktree-checkpoints.md).

For interruption, context loss, or ambiguous "continue" requests, read [references/interruption-recovery.md](references/interruption-recovery.md).

For long processes, background execution, server burn-in, or SSH, read [references/long-running-work.md](references/long-running-work.md).

For multi-Session, Goal, AgentTask, AgentWait, Conversation/Wake, or delegated-agent orchestration, read [references/orchestration.md](references/orchestration.md).

For testing, review, evidence, and acceptance gates, read [references/validation-audit.md](references/validation-audit.md).

For stage/phase closeout, retrospective, and cleanup, read [references/closeout-retrospective.md](references/closeout-retrospective.md).

For WebCodex capability discovery and downgrade behavior, read [references/webcodex-capabilities.md](references/webcodex-capabilities.md).

## Default controller loop

For a substantial task:

1. Resolve the exact Project and current durable context.
2. Verify the canonical predecessor/HEAD and workspace state.
3. Identify the next bounded unit of work and its acceptance evidence.
4. Create/reuse an isolated worktree when appropriate.
5. Inspect only the necessary code/data path; avoid broad rereads when a valid checkpoint/handoff exists.
6. Implement the bounded change.
7. Run focused validation.
8. Review the exact diff and workspace hygiene.
9. Commit the validated unit; push when it is an important recovery boundary.
10. Record/update the next exact action in durable project state when practical.
11. Continue without asking the user unless a true decision boundary is reached.
12. At major gates, run an independent audit/affected validation before promotion.

## Decision boundaries

Stop and ask for explicit authorization when the next action would change a frozen architecture/scope/acceptance contract, accept a material unresolved risk, perform destructive cleanup, or merge to a protected/default branch when the project policy reserves that decision for the user.

Do not stop for ordinary inspection, bounded implementation, tests, review-branch commit/push, safe worktree creation, or continued observation of already-started work.

## Recovery invariant

After any interruption, first recover identity and evidence, then continue only the uncompleted delta. Never begin by "reading the whole repository again" unless durable recovery evidence is missing or stale.
