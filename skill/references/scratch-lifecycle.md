# Scratch and Resource Lifecycle

## Purpose

Keep WebCodex-created temporary state out of authoritative project/user workspaces and make every material temporary resource recoverable and reclaimable.

Scratch is Runner-local owned working state, not a second source tree and not a permanent artifact store. The primary rule is:

> allocate with ownership -> work -> promote durable results -> finalize -> reclaim -> verify

Do not rely on later path scanning as the normal cleanup mechanism.

## Contents

- [Configured roots and placement admission](#configured-roots-and-placement-admission)
- [Project/task layout](#projecttask-layout)
- [Resource ownership manifest](#resource-ownership-manifest)
- [Retention classes](#retention-classes)
- [Build and dependency outputs](#build-and-dependency-outputs)
- [Evidence promotion](#evidence-promotion)
- [Interruption and recovery](#interruption-and-recovery)
- [Terminal finalization](#terminal-finalization)
- [Pre-allocation reconciliation](#pre-allocation-reconciliation)
- [Hygiene, orphan recovery, and capacity](#hygiene-orphan-recovery-and-capacity)
- [Multi-Runner rule](#multi-runner-rule)

## Configured roots and placement admission

For this installation, the pre-authorized WebCodex scratch roots are:

- macOS: `/Users/youzai/ai/scratch`
- Windows: `D:\ai\scratch`

These are deployment-specific roots, not universal WebCodex defaults.

Use the configured scratch root automatically for WebCodex-created ephemeral state such as:

- non-Git native-validation workspaces;
- copied/extracted source used only for validation;
- transfer packaging and unpacking;
- Browser downloads and staging;
- one-off scripts and transient logs;
- temporary screenshots or raw evidence;
- task-scoped build/dependency output when the project/toolchain permits it.

Do **not** place WebCodex-created temporary state in a source checkout, Desktop, Downloads, drive root, a convenient user project directory, or another arbitrary persistent location merely because that path is writable.

A non-scratch destination is allowed only when at least one is true:

1. project/repository instructions explicitly own that destination;
2. the user explicitly approved that destination for this resource class;
3. the destination is the authoritative source/artifact location required by the task.

If a new persistent or user-visible destination is not already authorized, explain what would be stored there and why, then obtain the required user decision before creating it.

## Project/task layout

Use one stable project directory under the Runner-local scratch root:

~~~text
scratch/
└── <readable-project-name>--<stable-project-key>/
    ├── project.json
    ├── shared/
    └── tasks/
        └── <task-key>/
            ├── manifest.json
            ├── source/
            ├── build/
            ├── downloads/
            ├── staging/
            ├── screenshots/
            ├── logs/
            └── misc/
~~~

Create subdirectories lazily. A validation source copy belongs under the owning task rather than beside the user's normal project files.

Derive the stable project key from an exact durable WebCodex Project or other authoritative project identity. Never guess durable scratch identity from a display name alone.

## Resource ownership manifest

Creation and cleanup use explicit provenance, not path heuristics.

A task `manifest.json` should remain small and mechanical and may track one or more owned resources. For each disk-material resource, retain enough fields to establish:

- resource id/kind;
- `created_by_webcodex` provenance;
- exact Project and strongest available Task/Session/Job/run owner;
- Runner identity;
- exact path;
- source/candidate/ref/hash when relevant;
- retention class;
- lifecycle state;
- cleanup triggers;
- cleanup finalizers/blockers;
- promoted durable artifact/evidence locations.

Useful lifecycle states include:

~~~text
active
waiting
recovery_required
terminal
finalizing
cleanup_pending
closed
~~~

Do not invent a second project/task database. The manifest exists only to prove ownership, recovery requirements, and end-of-life.

If ownership metadata is missing or inconsistent, protect the resource and reconcile/ask rather than broad-scan deleting nearby files.

## Retention classes

Classify WebCodex-managed filesystem state by retention, not by filename.

### Runner temporary

Runtime-internal temporary files remain runtime-owned. Do not copy them into scratch merely to track them.

### Owned ephemeral

Examples: validation source copies, transfer archives, unpacked intermediates, debug screenshots, one-off scripts, transient logs.

Default: reclaim after the exact owner is safely terminal and required results are promoted.

### Owned regenerable

Examples: `target/`, build/intermediate output, dependency trees, generated `dist/`/out directories, task-scoped caches.

Default: reclaim when no immediate dependent needs them. Retaining the source/worktree never implies retaining regenerable state.

### Recovery-required

State still required to resume active, waiting, interrupted, blocked, or outcome-unknown work.

Default: retain until the exact prior effect is reconciled and another durable recovery path exists.

### Pending promotion

Raw material that may become formal evidence/artifact.

Default: promote the minimum required durable result or delete it at finalization.

### Durable project-owned

Authoritative source, project-declared evidence, or promoted artifacts leave scratch semantics and follow their owning project policy.

### Foreign/unknown

Pre-existing or ownership-uncertain state is never treated as owned scratch merely because it looks temporary. Protect and escalate for a decision when cleanup is desired.

## Build and dependency outputs

Generated output has a lifecycle independent from its source checkout/worktree.

When a validation/build is ephemeral and the toolchain supports a documented per-process output location without violating project policy, prefer routing heavy generated state under the owning task scratch. For example, Cargo supports a task-specific target directory through its standard target-dir mechanisms.

Do not mutate global user/toolchain configuration merely to implement scratch policy, and do not invent a shared cross-worktree cache layout. Use project/toolchain-supported caching only when already authorized.

When output remains inside a checkout/worktree, still treat it as an owned regenerable resource and finalize it separately. In particular:

> keep worktree != keep target/build/dependencies

## Evidence promotion

Raw validation material starts as scratch unless the project already declares it durable.

Prefer promoting compact, reconstructable evidence such as:

- candidate/ref/hash;
- exact Job/Task/Attempt identity;
- result/verdict and test counts;
- required log excerpt/receipt;
- artifact hash/location;
- necessary screenshots.

A transport archive, extracted repository copy, dependency tree, or complete build directory is not formal evidence merely because it participated in validation.

Preserving failed formal evidence means preserving the required failed-run provenance/result. It does not automatically require retaining every reproducible build intermediate.

If a large binary must become durable evidence and no project-owned artifact destination exists, surface the proposed destination/retention before persisting it.

## Interruption and recovery

Do not clean an owned resource merely because a model turn, ChatGPT window, Host carrier, or Runner connection ended.

For active, waiting, interrupted, blocked, or outcome-unknown work:

1. recover exact owner/resource identity;
2. reconcile Task/Job/process state;
3. determine whether the resource is still the only recovery copy;
4. retain only while that recovery dependency remains real.

Cleanup itself must be retryable. If only some finalization steps succeed, record `cleanup_pending` and continue the unresolved cleanup delta later rather than recreating or broadly deleting resources.

## Terminal finalization

Substantive PASS/FAIL/SUPERSEDED/CANCELLED does not by itself close owned-resource lifecycle.

For an exact safely terminal owner:

1. pull back required results;
2. promote required durable evidence/artifacts;
3. verify no active Job/Task/process still depends on each resource;
4. verify no unique dirty/uncommitted/recovery state would be lost;
5. reclaim owned ephemeral and unneeded regenerable resources;
6. close/unregister temporary control-plane objects when appropriate;
7. verify expected path/registry/disk changes;
8. mark the resource lifecycle `closed`.

If a finalizer cannot be satisfied, leave the exact resource `cleanup_pending` with the blocker recorded.

## Pre-allocation reconciliation

Before creating another heavy worktree, validation workspace, source copy, or build for the same Project, inspect known owned leases/resources from prior tasks.

If earlier resources are already terminal or `cleanup_pending`, finish their safe cleanup first when possible. Do not keep allocating new large resources on top of known terminal leftovers.

This is a recovery guard, not permission for a broad filesystem sweep.

## Hygiene, orphan recovery, and capacity

Normal cleanup is manifest/ownership scoped.

Use broader scratch hygiene only as a fallback to find:

- terminal manifests whose cleanup never completed;
- orphaned WebCodex-owned task directories;
- stale recovery-required state;
- pending-promotion evidence;
- oversized owned scratch;
- shared scratch with no live dependents.

Age/TTL may help identify candidates, but age alone never proves deletion safety. Automatic orphan cleanup is limited to WebCodex-owned scratch with recoverable ownership plus satisfied finalizers.

Keep workspace hygiene and scratch hygiene separate.

For this installation, about 2 GiB per task and 10 GiB per project remain useful soft review signals. If a Project is already above a soft threshold, report/reconcile existing owned terminal state before another large allocation. Thresholds are not deletion authority.

## Multi-Runner rule

The same logical Project may have independent scratch on Mac and Windows.

Record Runner identity on every owned resource. Never infer that a path on one Runner exists on another, and never transfer temporary trees merely to mirror layouts. Transfer only what the cross-Runner task actually needs; keep transport/extracted copies owned by their exact source/destination tasks and finalize both sides after handoff.
