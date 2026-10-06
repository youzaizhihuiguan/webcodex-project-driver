# Stage 1 Lessons That Motivated This Project

This repository was born from a multi-day KeyQuant Stage 1 implementation, validation, remediation, Soak, audit, and closeout cycle.

The purpose of this archive is not to reproduce KeyQuant-specific business logic. It records workflow lessons that generalize.

## 1. Chat context is not durable engineering state

Long ChatGPT turns were vulnerable to truncation or host-side "processing" states. Recovery became expensive when the only record of the next step lived in the conversation.

The durable recovery chain became:

```text
exact Session
-> exact remote ref / commit
-> git status
-> validation/evidence
-> running Job identity
-> only then continue the delta
```

## 2. Worktree isolation matters

Multiple remediation, audit, and failed-Soak lines needed to coexist. Worktrees prevented branch switching and uncommitted state from contaminating another task.

Important distinction:
- worktree deletion;
- branch deletion;
- commit reachability;
- remote branch deletion

are separate operations.

## 3. Commit and push are recovery primitives

A useful commit is not merely a historical record. It is a machine-verifiable recovery boundary.

Good checkpoints are:
- bounded;
- validated;
- explainable;
- independently reviewable;
- pushed when important.

## 4. Failed windows are evidence

Formal failure windows were preserved instead of overwritten or resumed. A code fix did not retroactively convert the old failure to PASS.

This protected denominator integrity and made later auditing possible.

## 5. Acceptance logic also needs auditing

The system under test is not the only source of bugs. Runner lifecycle, fail-fast math, denominator accounting, metadata drift, and admission checks can all invalidate a formal window.

Therefore acceptance machinery should be reviewed as production logic.

## 6. Failure classes must stay distinct

Examples encountered:
- external hosting/source behavior;
- transport/network failures;
- third-party exception hierarchy surprises;
- parser/schema failures;
- product correctness defects;
- runner/control defects.

Treating all of them as "code bugs" creates bad remediation.

## 7. Dependency behavior must be tested, not assumed

A concrete example was a timeout type derived from `BaseException` rather than ordinary `Exception`, escaping a boundary that looked correct by inspection.

Third-party async/network libraries deserve failure-shape tests before long formal runs.

## 8. Test identity/history isolation matters

A fault test can pollute later history- or replay-sensitive tests when they reuse the same persistent identity. History/fault/concurrency tests should default to disposable namespaces or synthetic identities.

## 9. Do not repeatedly reread the whole repository

After a checkpoint exists, recovery should inspect the exact delta and recorded evidence. Re-running broad discovery after every interruption wastes time and can introduce new interpretation drift.

## 10. Audit and implementation should be separate roles

Independent read-only audit found issues that implementation-focused execution had not surfaced. Auditors should not casually mutate the same worktree they are reviewing.

## 11. Long runtime and model-turn lifetime are different

A one-hour Soak should not require one one-hour model turn. Long execution needs its own runtime identity and manifest.

## 12. A browser window is not a Session

A practical test attempted to leave a message in one exact WebCodex Session and later "continue" in a browser window. The window resumed a different Session and did unrelated closeout work.

This produced a hard rule:
**never infer Workflow Session identity from a browser tab.**

## 13. Resolved backend work is not the same as user-visible delivery

Another test successfully produced and stored a Session answer and resolved the original message, but the final browser reply only summarized that completion instead of presenting the answer body.

Controllers must fetch and surface delegated results, not merely report IDs/status.

## 14. Engineering closeout and strict stability acceptance are different states

A project may close an engineering phase while retaining a strict formal failure as historical evidence and explicitly accepting an operational risk. Do not relabel the original failure.

## 15. The resulting execution philosophy

```text
Plan
-> exact baseline
-> bounded task
-> isolated execution
-> focused validation
-> checkpoint
-> continue
-> independent audit at major gate
-> immutable failure evidence
-> closeout
```

The project lifecycle may be long. Each individual model turn should stay small enough to recover cheaply.
