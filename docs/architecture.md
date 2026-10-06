# Architecture

## Problem

Substantial WebCodex work may outlive a single model turn and may involve durable Sessions, Jobs, Goals/Tasks, resources, artifacts, evidence, and changing runtime capabilities.

The controller therefore cannot treat chat memory or a browser window as authoritative execution state.

## Core state model

For every stateful WebCodex effect, separate:

```text
durable identity
+
freshness / generation proof
+
authority
```

Examples:

- identity: Project, Session, Goal, Task, Job, page, resource;
- freshness: assignment fence, Attempt generation, snapshot/ref, observation token, replay selector;
- authority: project/runtime/user permission for the requested effect.

One does not substitute for another.

## Universal controller loop

```text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
```

### OBSERVE

Read the exact current state needed for the next decision, including live capability readiness when an optional backend is under consideration.

### RECONCILE

If prior execution may already exist, inspect the exact existing identity before creating replacement work.

### ACT

Perform one bounded authorized effect with current identity/freshness/authority.

### VERIFY

Re-observe enough state to prove the intended transition or preserve explicit uncertainty.

### PERSIST / HANDOFF

When recovery matters, durably record:

- objective;
- phase/status;
- active identities;
- evidence/results;
- resource ownership;
- last verified state;
- exact next action;
- decision blockers.

## Objective authority

A durable control plane does not create its own business/domain objective.

If the user/project has not defined the actual next objective, repository contents are not permission to invent:

- implementation tasks;
- evidence;
- branches;
- pushes;
- experiments;
- other external mutations.

Missing objective is a decision blocker unless an authoritative project contract already defines the next action.

## Composition

Subject to platform/runtime authority:

```text
project-local explicit contract
> domain Skill domain-quality rules
> Project Driver generic control heuristics
```

Project Driver still owns WebCodex identity/freshness/recovery semantics.

## Software adaptation

Git commit/ref/worktree state is authoritative when the target project uses Git as a source-of-truth substrate.

In that case, software work may adapt the universal loop with:

- exact HEAD/ref/status observation;
- managed worktree isolation;
- focused project-owned validation;
- bounded commit/checkpoint;
- review branch push;
- Git-aware cleanup.

These are not universal requirements for research, browser, data, artifact, or other non-Git workflows.

## Long-running work

Long execution gets its own durable identity.

Do not keep a model turn open merely because a process is long. Choose Runner-owned Job, async Job, detached supervisor process, persistent shell, or another primitive according to lifecycle and ownership requirements, then recover the same identity later.

## Capability gating

Tool/API exposure is not the same as configured readiness.

Volatile tool schemas, providers, Host continuation readiness, Browser/Computer support, SSH resources, plugins, LSP, and similar optional paths come from live runtime observation rather than static Skill copies.

## Evidence and closeout

Control-plane completion requires more than "task resolved":

- evidence must belong to the intended run/candidate;
- failed formal evidence is preserved;
- delegated result bodies/artifacts are pulled back;
- resources are handed off/released deliberately;
- exact next action remains durable when work continues.

## Future direction

Durable Goal/Agent orchestration and Host continuation remain optional capability-gated paths until demonstrated end-to-end in the active environment.
