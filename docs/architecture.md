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

## WebCodex control loop

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

## Objective and operating-model authority

A durable WebCodex control plane does not own generic project objective/scope policy.

Project-local instructions and, when active, `agent-operating-model` own bounded-objective, no-invented-gates, proportional-rigor, generic recovery/verification, and material-mutation guardrails.

Project Driver maps the authorized work onto exact WebCodex identities, freshness proofs, resources, placements, waits, and lifecycle state.

## Capability coverage

The live WebCodex runtime is the volatile source of truth for tool families, schemas, provider inventories, Runner capabilities, and Host continuation readiness.

Static Skill material stores stable selection rules, lifecycle semantics, safety/recovery invariants, and reusable orchestration patterns.

It intentionally does not mirror every current tool schema.

This allows new runtime tools to be admitted through live discovery without requiring a Skill rewrite when they fit an existing control pattern.

## WebCodex-native topology

Topology selection belongs to the outer task contract / operating model. Once a topology is justified, WebCodex can represent it as:

~~~text
controller
  -> worker(s)
  -> optional integrator
  -> optional auditor
~~~

A durable Goal may hold correlation/progress state. Durable Agent identity may outlive one window. AgentTask/Attempt may provide worker ownership/fencing. AgentWait may provide fan-in. CodingAgent or another backend performs execution only when current provider readiness and authority exist.

Worker completion, integration completion, audit acceptance, and user-visible delivery remain distinct states.

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

Responsibility is layered rather than duplicated:

~~~text
project/path instructions: project truth and policy
agent-operating-model: generic cross-cutting guardrails
domain Skills: domain methods/correctness
webcodex-project-driver: WebCodex-specific control semantics
WebCodex runtime: live schemas/capabilities/state
~~~

Actual instruction precedence remains host/platform semantics; this diagram describes ownership only.

## Software adaptation

When Git is authoritative, Project Driver may map WebCodex Projects onto exact checkout/worktree state.

Default to an existing suitable checkout. Create a managed worktree only for concrete isolation/concurrency/preservation needs; task size, review, or duration alone are insufficient. Reuse a compatible managed worktree when safe.

Repository/project policy owns ordinary commit/push/PR/release decisions. Project Driver owns WebCodex worktree identity, ownership, recovery, registry reconciliation, and Git-aware terminal cleanup.

Generated-output amplification is distinct from Git metadata. In this installation, the measured large worktree footprint was dominated by replicated Rust `target/` output.

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

The outer user/project contract or `agent-operating-model` owns generic continuation and material-decision boundaries.

Project Driver supplies the WebCodex facts needed for those decisions: exact identity, freshness, prior-effect reconciliation, provider/Host readiness, Runner/resource ownership, result provenance, and whether a verified platform fallback exists.
