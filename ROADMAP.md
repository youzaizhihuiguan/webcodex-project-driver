# Roadmap

## v0.1 — durable software-engineering workflow

Status: released baseline.

Established:

- exact Session/Project/Job recovery;
- short bounded batches;
- worktree/Git checkpoint discipline;
- long Job lifecycle;
- capability gating;
- result pullback;
- failure-evidence preservation;
- decision boundaries.

## v0.2 — WebCodex control plane

Status: implementation/review.

Goals:

- make `durable identity + freshness/generation proof + authority` the core state model;
- make `OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF` the universal loop;
- promote reconcile-before-retry to a core invariant;
- forbid invented work under ambiguous objectives;
- add cross-domain durable run state;
- define Project Driver versus domain Skill ownership;
- keep volatile runtime schemas in live manifests;
- move Git/worktree/checkpoint semantics into a software-specific adaptation;
- preserve routing behavior unless real eval evidence justifies change.

Promotion uses focused regressions rather than repeating already-proven broad smoke coverage.

## v0.3 — durable Goal workflow

Experiment with:

- Goal admission;
- Goal checkpoints;
- exact Session correlation;
- recovery in a new chat/window;
- controller state that survives conversation truncation.

Do not promote Goal workflow to mandatory until recovery behavior is demonstrated end-to-end.

## v0.4 — Agent orchestration

When a configured execution provider is actually available:

- durable Controller Agent;
- AgentTask + Attempt + freshness fencing;
- delegated execution;
- AgentWait fan-out/fan-in;
- result reconciliation and pullback.

## v0.5 — Host continuation

Validate Host continuation end-to-end rather than assuming API exposure equals wake readiness.

## v1.0 — stable multi-domain WebCodex control plane

Requirements:

- validated across multiple unrelated projects/workflow types;
- interruption/uncertain-outcome reconciliation tested;
- long-job recovery tested;
- optional capability downgrade paths tested;
- low harmful false-trigger rate;
- clear composition with domain Skills;
- stable package/release process.

Do not turn the Skill into a universal monolith.
