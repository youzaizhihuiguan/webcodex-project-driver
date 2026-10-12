# Scratch Lifecycle

## Purpose

Keep recoverable construction debris out of authoritative project workspaces while preserving enough temporary state to survive interruption.

Scratch is not a second source tree and not a permanent artifact store. It is short-to-medium-lived, Runner-local working state owned by an exact Project and bounded Task/Session/Job/run.

## Contents

- [Configured roots](#configured-roots)
- [Project layout](#project-layout)
- [Stable project identity](#stable-project-identity)
- [Project metadata](#project-metadata)
- [Task ownership](#task-ownership)
- [Lifecycle classes](#lifecycle-classes)
- [Computer / Browser / script hygiene](#computer--browser--script-hygiene)
- [Shared scratch](#shared-scratch)
- [Interruption rule](#interruption-rule)
- [Closeout and cleanup](#closeout-and-cleanup)
- [Hygiene and capacity](#hygiene-and-capacity)
- [Multi-Runner rule](#multi-runner-rule)

## Configured roots

For this installation, use:

- macOS: `/Users/youzai/ai/scratch`
- Windows: `D:\ai\scratch`

Treat these as user-selected deployment roots, not universal WebCodex defaults. A different Runner must have an explicitly configured scratch root before this policy is relied on.

Scratch roots are Runner-local. Do not assume the macOS and Windows roots are the same filesystem or automatically synchronized.

## Project layout

Use one stable project directory under the Runner-local root:

~~~text
scratch/
└── <readable-project-name>--<stable-project-key>/
    ├── project.json
    ├── shared/
    └── tasks/
        └── <task-key>/
            ├── manifest.json
            ├── screenshots/
            ├── scripts/
            ├── downloads/
            ├── staging/
            ├── logs/
            └── misc/
~~~

Create task subdirectories lazily. Do not pre-create empty categories that the run never uses.

## Stable project identity

Resolve an exact WebCodex Project or other authoritative project identity before creating durable project scratch.

Derive the stable project key from an exact durable identity such as the canonical WebCodex Project identity or another project-owned stable identifier. Keep a readable project-name prefix only for human navigation.

If two projects share the same display name, their stable keys must still differ.

If project identity is materially ambiguous, do not create guessed durable scratch such as `project-2`, `temp-project`, or a directory inferred only from chat text.

When the exact Project is known and its scratch directory is absent, create the project scratch automatically when current authority permits it. This is routine control-plane housekeeping, not a user decision.

## Project metadata

Keep `project.json` small and mechanical. Record only fields that help recovery, for example:

- readable project name;
- exact project identity;
- canonical project path or repository identity when applicable;
- Runner/client identity;
- created/last-used timestamps;
- optional schema version.

Do not turn `project.json` into a second project database.

## Task ownership

Prefer one bounded Task/run directory per independently cleanable unit.

Use the strongest exact owner identity already available:

1. AgentTask;
2. Workflow Session;
3. Job;
4. another explicit run id created after Project identity is known.

Do not make Agent/model name the first-level partition. Multiple agents may collaborate on the same Project and Task.

A task `manifest.json` should record enough to recover ownership and cleanup state, such as:

- owner/controller kind;
- exact Project identity;
- exact Task/Session/Job/run identity;
- Runner identity;
- lifecycle state;
- created/last-used timestamps;
- `recovery_required`;
- promoted artifact/evidence locations when relevant.

## Lifecycle classes

Distinguish these classes:

### Runner temporary

Runtime-owned temporary files, such as the typed temporary script used internally by `run_script`, remain runtime-owned. Do not copy them into scratch merely to track them.

### Ephemeral scratch

Disposable construction outputs such as ordinary debug screenshots, one-off helper files, temporary JSON, download staging, unpacked intermediates, and transient logs.

Delete these after their owning task reaches a safely reconciled terminal state.

### Recovery-required scratch

Temporary state still needed to resume an active, waiting, blocked, interrupted, or outcome-unknown task.

Retain it until the exact owning work is reconciled and a durable replacement/checkpoint exists.

### Pending promotion

Temporary output that may become durable evidence/artifact, such as a failure screenshot, benchmark log, GUI acceptance image, or reproduction bundle.

At closeout, explicitly promote the useful result into the authoritative artifact/evidence location or delete it.

### Durable artifact/evidence/source

Once promoted into project-owned durable state, it leaves scratch cleanup semantics. Do not use scratch as its permanent home.

## Computer / Browser / script hygiene

Normal Computer observation should remain observation. Do not persist every UI step as an image.

Save a Computer snapshot only when it materially supports:

- interruption recovery;
- failure or audit evidence;
- final GUI acceptance;
- a user-requested screenshot;
- a cross-turn visual state that cannot be reconstructed cheaply.

Place scratch screenshots under the owning task until promoted.

Place agent-created one-off scripts, Browser downloads, unpacking/conversion staging, debug logs, and similar recoverable debris under the owning task scratch rather than the source Project, Desktop, Downloads, drive root, or arbitrary system directories.

Prefer Runner-owned temporary execution for truly disposable scripts when recovery does not require the file.

## Shared scratch

Use `shared/` only for temporary material genuinely required by multiple bounded tasks in the same Project.

Do not use `shared/` as a miscellaneous dumping ground. Track owners/dependents when shared scratch materially affects recovery.

## Interruption rule

Do not clean scratch merely because a model turn, ChatGPT window, Host carrier, or Runner connection ended.

For `active`, `waiting`, `blocked`, `interrupted`, or outcome-`unknown` work:

1. recover exact ownership;
2. reconcile Task/Job/resource state;
3. determine whether scratch remains the only recovery copy;
4. clean only after a durable replacement or terminal outcome is verified.

## Closeout and cleanup

For a safely reconciled terminal task:

1. inspect its manifest and exact owner;
2. promote required evidence/artifacts;
3. verify no active worker/run still depends on its scratch;
4. delete remaining ephemeral/recovery scratch;
5. prefer removing the entire task directory as the cleanup unit;
6. update project/shared references if needed.

For a retired Project scratch directory, delete it only after no active/recoverable work or unique evidence remains.

Unknown untracked files are not automatically scratch merely because they look temporary.

## Hygiene and capacity

Keep project-workspace hygiene and scratch hygiene separate.

Project-workspace hygiene looks for accidental debris inside the authoritative workspace.

Scratch hygiene looks for:

- terminal task leftovers;
- orphaned task/project directories;
- stale recovery-required state;
- pending-promotion evidence;
- oversized scratch;
- shared scratch with no live dependents.

Use capacity thresholds only as review triggers, not deletion authority. For this installation, useful initial soft-review thresholds are about 2 GiB per task and 10 GiB per project. Project policy may override them.

## Multi-Runner rule

The same logical Project may have independent scratch on Mac and Windows.

Record Runner identity and never infer that a scratch path on one Runner exists on another. Transfer only explicitly promoted/verified artifacts when cross-Runner sharing is required.
