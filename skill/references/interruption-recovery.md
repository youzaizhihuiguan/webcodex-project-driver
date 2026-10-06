# Interruption and Recovery

## Do not infer from the browser tab

A ChatGPT window may resume or be associated with a different Workflow Session than expected.

Bad:
- "continue in the audit window";
- "use the previous tab";
- "pick up where you left off".

Good:
- resume exact `wc_sess_...`;
- inspect exact Goal/Task/Job IDs;
- verify exact Project and Git state.

## Recovery sequence

After truncation, host interruption, a new window, or missing context:

1. resolve exact Project;
2. list/recover Sessions only if the exact Session is genuinely unknown;
3. explicitly select/resume the correct Session;
4. read unresolved assignment/message state;
5. inspect HEAD/ref/status;
6. inspect known Job identities;
7. inspect latest validation/evidence;
8. continue only the missing delta.

## Never duplicate uncertain work

If an operation may already have started:
- observe/reconcile the existing identity;
- reuse idempotency/replay keys when the contract requires them;
- do not create a replacement Job/Task merely because the previous response was lost.

## Result delivery

A backend task may be complete while the user-visible chat only reports status.

After delegated/session work completes:
1. fetch the answer/result body;
2. verify it corresponds to the expected task;
3. surface the substantive result to the user;
4. then report durable IDs/status as supporting metadata.

Do not make the user manually retrieve the result from a Session ledger.
