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

## v0.3.1 — operational hardening

Status: implementation/review.

Add:

- shared cross-agent scratch policy with Runner-local roots;
- stable Project/task ownership and lazy scratch creation;
- interruption-safe scratch retention and terminal promote-or-delete cleanup;
- Computer/Browser/script/download debris hygiene;
- durable attention routing for completion, failure, interruption, blockers, and user decisions;
- focused behavior evals B19-B25.

Keep the v0.3 trigger and control-plane architecture unchanged.

## v0.3.2 — composition split and managed-worktree hardening

Status: implementation/validation.

Goals:

- compose cleanly with the generic `agent-operating-model` Skill;
- remove or narrow generic project/software methodology now owned elsewhere;
- preserve all WebCodex-specific identity, freshness, runtime, recovery, resource, and evidence semantics;
- default managed-worktree selection to an existing suitable checkout;
- require concrete isolation/concurrency/preservation value before creating another worktree;
- support safe managed-worktree reuse and Git/WebCodex-aware terminal cleanup;
- treat build-output amplification separately from Git worktree metadata;
- validate low-ceremony composition without weakening uncertain-outcome recovery.

## v0.3.3 — resource lifecycle hardening

Status: implementation/validation.

Goals:

- admit disk-material WebCodex resources with exact owner, placement, retention class, cleanup condition, and applicable authority before allocation;
- require configured Runner scratch for WebCodex-created non-Git validation workspaces, transfer staging, copied/extracted source, and similar temporary state unless the project/user owns another destination;
- record recoverable provenance for managed worktrees and other owned ephemeral resources rather than inferring ownership from paths later;
- treat fresh/read-only review as reasoning independence, not automatic filesystem isolation;
- separate worktree/source retention from build/dependency/cache/transport retention;
- stage raw evidence in scratch and promote only required durable results;
- make owned-resource finalization part of terminal lifecycle, with explicit `cleanup_pending` recovery when finalizers cannot complete;
- reconcile known terminal owned leftovers before another heavy allocation;
- preserve unknown/foreign/dirty/unique state by default and forbid broad-discovery deletion as a substitute for provenance.

Validate against the real LlamaLab failure modes that produced replicated review worktrees, oversized Cargo output, non-Git Windows validation copies outside scratch, stale Sessions/Projects, and unfinalized transfer/evidence debris.

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
