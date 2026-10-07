# Roadmap

## v0.1 — durable software-engineering workflow

Status: released baseline.

Established exact Session/Project/Job recovery, short bounded batches, Git/worktree checkpoints, long Job lifecycle, capability gating, result pullback, failure-evidence preservation, and decision boundaries.

## v0.2 — WebCodex control plane

Status: review-ready baseline.

Established:

- durable identity + freshness/generation proof + authority;
- OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF;
- reconcile-before-retry;
- ambiguous-objective non-invention;
- cross-domain durable run state;
- domain/project ownership boundaries;
- live runtime schema/capability discovery;
- software-specific Git adaptation.

Focused Host regressions and package provenance are recorded.

## v0.3 — WebCodex-native orchestration

Status: implementation/review.

Goals:

- cover the complete live WebCodex capability surface through dynamic discovery rather than a static tool catalog;
- add Supervisor -> Worker(s) -> optional Integrator -> independent Auditor topology;
- formalize AgentTask/Attempt/AgentWait fan-out/fan-in;
- formalize event-driven Job/Agent continuation and Host readiness gating;
- add multi-Runner placement/fleet rules;
- add Browser/Computer/SSH/artifact cross-surface patterns;
- add cross-Project artifact/integration flow;
- include Runner Skill/Plugin/local-MCP capability extension;
- add autonomous remediation/escalation policy;
- extend durable run state and evidence provenance for multi-Agent/multi-Runner recovery.

Do not broaden trigger metadata merely because more runtime capabilities are covered.

## v0.4 — live delegated-agent execution validation

Validate the v0.3 orchestration patterns end-to-end when a real CodingAgent provider and wake-capable Host continuation path are configured:

- durable Controller Agent;
- multiple AgentTasks/Attempts;
- provider-backed delegated workers;
- AgentWait fan-in;
- automatic controller re-entry;
- integration + independent audit;
- interruption/recovery during parallel work.

Do not claim this as proven while the active Runners advertise no CodingAgent provider.

## v0.5 — fleet and long-horizon automation

Validate:

- Mac/Windows/remote placement policies;
- cross-platform integration matrices;
- long-horizon Goal/controller recovery;
- cross-Project artifact pipelines;
- capability installation/rollback workflows;
- evidence graph/reporting;
- bounded cost/concurrency policies where available.

## v1.0 — stable WebCodex-native project control plane

Requirements:

- validated across multiple unrelated projects/workflow types;
- delegated and non-delegated orchestration both tested;
- interruption/uncertain-outcome reconciliation tested;
- long-job and wake recovery tested;
- multi-Runner placement tested;
- optional capability downgrade paths tested;
- low harmful false-trigger rate;
- clear composition with domain Skills;
- stable package/release process.

Do not turn the Skill into a universal domain monolith or a frozen copy of WebCodex's tool registry.
