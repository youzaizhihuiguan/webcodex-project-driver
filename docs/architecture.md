# Architecture

## Problem

Substantial WebCodex work may outlive a single model turn and may involve durable Sessions, Jobs, Goals/Tasks, Agents, Runners, resources, artifacts, evidence, multiple UI surfaces, and changing runtime capabilities.

The controller therefore cannot treat chat memory, one browser window, or one checkout as authoritative execution state.

## Core state model

For every stateful WebCodex effect, separate:

~~~text
durable identity
+
freshness / generation proof
+
authority
~~~

Examples:

- identity: Project, Session, Goal, Agent, Task, Attempt, Job, page, artifact, resource;
- freshness: assignment fence, Attempt generation, Endpoint generation, snapshot/ref, observation token, replay selector, file revision;
- authority: project/runtime/user permission for the requested effect.

One does not substitute for another.

## Universal controller loop

~~~text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
~~~

### OBSERVE

Read the exact current state needed for the next decision, including live capability/provider/Host readiness and placement state when relevant.

### RECONCILE

If prior execution may already exist, inspect the exact existing identity before creating replacement work.

### ACT

Perform one bounded authorized effect with current identity/freshness/authority.

### VERIFY

Re-observe enough state to prove the intended transition or preserve explicit uncertainty.

### PERSIST / HANDOFF

When recovery matters, durably record objective, phase, identities, topology/dependencies, placement, evidence/results, resources, last verified state, integration/audit state, exact next action, and decision blockers.

## Objective authority

A durable control plane does not create its own business/domain objective.

If the user/project has not defined the actual next objective, repository contents are not permission to invent implementation tasks, evidence, branches, pushes, experiments, or other external mutations.

Missing objective is a decision blocker unless an authoritative project contract already defines the next action.

## Capability coverage

The live WebCodex runtime is the volatile source of truth for tool families, schemas, provider inventories, Runner capabilities, and Host continuation readiness.

Static Skill material stores stable selection rules, lifecycle semantics, safety/recovery invariants, and reusable orchestration patterns.

It intentionally does not mirror every current tool schema.

This allows new runtime tools to be admitted through live discovery without requiring a Skill rewrite when they fit an existing control pattern.

## WebCodex-native topology

Default:

~~~text
single controller
~~~

When justified:

~~~text
Supervisor / Controller
        |
        +-- Worker(s)
        |
        +-- optional Integrator
        |
        +-- independent Auditor
~~~

A durable Goal may hold phase/progress. Durable Agent identity may outlive one window. AgentTask/Attempt may provide worker ownership/fencing. AgentWait may provide fan-in. CodingAgent or another backend performs execution only when current provider readiness and authority exist.

Worker completion, integration completion, and audit acceptance are distinct states.

## Event-driven continuation

When supported, use durable Job waits, AgentWait, Endpoint/Wake, or equivalent Host continuation so a controller does not spend one giant model turn polling.

Auto-resume is capability-gated. Endpoint/API existence does not prove a production Host carrier is ready.

When no wake path is ready, persist the exact identities/state and recover them in a later turn.

## Runner placement

For multi-Runner/fleet execution, choose placement from:

1. authority and project/resource accessibility;
2. required platform/capability;
3. project/data/resource locality;
4. lifecycle/restart requirements;
5. current concurrency/load;
6. recovery/integration cost.

Do not silently migrate project state merely because another Runner looks idle.

## Cross-surface operations

Browser, Computer, persistent shells/SSH, artifacts, and Project-to-Project transfers follow the same identity/freshness/authority loop.

Examples:

- Browser navigation invalidates stale element authority;
- Computer launch/window changes require fresh observation;
- persistent shell identity is separate from remote host identity;
- artifact transfer should preserve snapshot/content provenance;
- cross-Project transfer success is not integration success.

## Composition

Subject to platform/runtime authority:

~~~text
project-local explicit contract
> domain Skill domain-quality rules
> Project Driver generic control heuristics
~~~

Project Driver still owns WebCodex identity/freshness/recovery/orchestration semantics.

## Software adaptation

Git commit/ref/worktree state is authoritative when the target project uses Git as a source-of-truth substrate.

In that case, software work may adapt the universal loop with exact HEAD/ref/status observation, managed worktree isolation, project-owned validation, bounded commit/checkpoint, review branch push, and Git-aware cleanup.

These are not universal requirements for non-Git workflows.

## Long-running work

Long execution gets its own durable identity.

Choose Runner-owned Job, immediate async Job, detached supervisor process, persistent shell, delegated run, or another primitive according to form, lifecycle, ownership, and restart requirements.

Duration alone is not a reason to detach.

## Integration and evidence

For parallel work, maintain provenance from objective -> Task/Attempt -> output -> candidate/artifact -> validation -> integration -> audit.

Several passing workers do not prove the combined candidate.

A final acceptance claim should be traceable to the exact candidate and evidence.

## Capability extension

Runner Skills, Skill resources, Plugins, and authorized local MCP providers may extend execution.

Discover them live. Installing/activating a Skill revision, changing Runner configuration, or binding a new provider is a distinct management effect with its own authority and rollback considerations.

## Evidence and closeout

Control-plane completion requires more than "task resolved":

- evidence belongs to the intended run/candidate;
- failed formal evidence is preserved;
- delegated result bodies/artifacts are pulled back;
- integration is explicit when required;
- independent audit is explicit when required;
- resources are handed off/released deliberately;
- exact next action remains durable when work continues.

## Automation boundary

Routine implementation, testing, safe remediation, observation, reconciliation, worker coordination, and evidence persistence may continue automatically inside an authorized frozen contract.

Architecture/scope changes, material risk acceptance, destructive history/resource operations, protected/default-branch promotion/release, or irreversible external actions remain decision boundaries unless project policy explicitly grants that authority.
