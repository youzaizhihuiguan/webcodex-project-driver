# Interruption and Recovery

## Identity is not window position

A ChatGPT window/tab, recent Project activity, or a phrase such as "the previous task" does not uniquely identify a Workflow Session, Goal, Task, Job, or resource.

Prefer exact durable identifiers and authoritative handoff state.

## Recovery sequence

After truncation, host interruption, a new window, uncertain tool delivery, or missing context:

1. resolve the required WebCodex Project/execution context;
2. recover exact known durable identities from the current handoff/run state;
3. if identity is genuinely unknown, discover candidates narrowly and reconcile them before mutation;
4. inspect unresolved assignment/message/task state relevant to the intended objective;
5. inspect known active Jobs/resources before redispatch;
6. verify the latest evidence and last known state;
7. continue only the missing authorized delta.

For Git-based software recovery, additionally use [software-git-adaptation.md](software-git-adaptation.md).

## Uncertain outcome -> reconcile before retry

If an operation may already have started or committed an effect:

- observe/reconcile the exact existing identity;
- reuse the live contract's idempotency/replay key when applicable;
- treat stale fences/generations/snapshots as invalid until refreshed;
- do not create a replacement Job/Task/resource merely because the response was lost;
- if the effect cannot be proven either way, preserve the uncertainty explicitly and choose a safe reconciliation path.

This rule applies to transport timeouts, lost model responses, Browser/Computer actions, Session assignment completion, Task attempts, Job handoff, artifact transfer, and other stateful effects.

## Ambiguous continuation

If the user says only "continue" and no exact unfinished objective can be recovered from authoritative durable state:

- do not choose work based on repository contents;
- do not create evidence, branches, pushes, experiments, or write tasks to manufacture progress;
- report the missing objective/identity as the blocker.

## Result delivery

Backend completion and user-visible delivery are separate checks.

After delegated/session work completes:

1. fetch the substantive result body or artifact;
2. verify it corresponds to the intended assignment/task;
3. surface the result to the user;
4. use IDs/status only as supporting metadata.

Do not make the user manually retrieve the result from a Session ledger.
