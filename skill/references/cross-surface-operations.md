# Cross-Surface and Cross-Project Operations

## Browser

Use:

~~~text
observe
-> act using current admitted identities
-> detect navigation/document/uncertainty
-> re-observe
-> verify
~~~

A stale element/snapshot is not authority for a later document.

For multi-step form/workflow actions, use the runtime's current batching semantics only while the same snapshot/document contract remains valid.

Place Browser downloads or other agent-created recoverable intermediates in the owning task scratch rather than an authoritative source directory, Desktop, Downloads, or arbitrary drive root unless the project explicitly owns that destination.

## Computer / desktop GUI

Before a control effect, observe the exact application/window/display/accessibility state required for that action.

After application launch, window activation, major UI transition, or uncertain effect, re-observe before relying on earlier UI state.

Tie GUI verification evidence to the exact build/candidate under test.

Ordinary Computer observation should not persist a screenshot by default. Save a snapshot only when recovery, failure/audit evidence, final GUI acceptance, or an explicit user request justifies persistence. Keep unpromoted snapshots in the owning task scratch; see [scratch-lifecycle.md](scratch-lifecycle.md).

## GUI QA pattern

~~~text
candidate/build
-> launch/open target
-> fresh UI observation
-> bounded interaction
-> re-observe
-> capture result/evidence
-> compare through project/domain acceptance method
~~~

Build PASS and GUI PASS are separate evidence.

## SSH / persistent shell

Use a managed SSH resource/persistent Session shell when the same remote process state, cwd, environment, exports, functions, or interactive context must persist.

Use one-shot remote execution when persistence is unnecessary.

Keep remote host/resource identity, persistent shell identity, and Job/process identity separate.

## Artifact transfer

Prefer the runtime's artifact transfer/handoff primitives for durable binary or large cross-Project results rather than passing bytes through model text.

When provenance matters, verify:

- source Project/artifact identity;
- frozen snapshot/content hash;
- destination Project/path;
- destination content/hash;
- overwrite/replay semantics.

Transfer success proves transport, not domain correctness.

## Cross-Project integration

A useful pattern:

~~~text
Project A result/artifact
        |
Project B result/artifact
        |
        v
Integration Project / candidate
        |
validation
        |
independent audit
~~~

Each Project keeps independent authority. Goal/Task correlation does not automatically grant cross-Project read/write access.

## External actions

Browser/Computer/remote operations may cross into irreversible external effects.

Treat purchases, submissions, destructive admin changes, publishing, release, or equivalent effects as decision boundaries unless the project/user has explicitly authorized that class of action.
