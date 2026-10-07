# Changelog

## 0.3.0 - 2026-10-07

### Added
- full live WebCodex capability coverage contract without statically copying the runtime tool registry;
- Supervisor -> Worker(s) -> optional Integrator -> independent Auditor orchestration pattern;
- durable Agent/AgentTask/Attempt/AgentWait fan-out/fan-in guidance;
- multi-Runner placement and fleet selection rules;
- event-driven Job/Agent continuation with Host readiness gating;
- Browser/Computer/SSH/artifact cross-surface patterns;
- cross-Project artifact/integration flow;
- Runner Skill/Plugin/local-MCP extension policy;
- autonomous remediation/escalation policy;
- multi-Agent/multi-Runner durable-state and evidence-provenance fields;
- focused behavior evals B12-B18 for the new orchestration risks.

### Preserved
- v0.2 routing description and core control invariants;
- live runtime manifests as the volatile schema/provider source of truth;
- software-specific Git adaptation rather than universal Git semantics.

## 0.2.0 - 2026-10-07

### Changed
- redefined the Skill as a WebCodex durable control plane rather than a software-engineering workflow;
- adopted `durable identity + freshness/generation proof + authority` as the core state model;
- adopted `OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF` as the universal loop;
- promoted reconcile-before-retry for uncertain outcomes;
- added an explicit rule that ambiguous objectives do not authorize invented work;
- added cross-domain durable run state and composition/ownership boundaries;
- moved Git/worktree/checkpoint rules into a software-specific adaptation;
- made live runtime manifests authoritative for volatile WebCodex schemas/capability readiness;
- preserved exact Session/Job identity, bounded batches, provider gating, result pullback, failure evidence, and decision boundaries.

### Evaluation
- incorporated real host observations for T03, T07, N01, N08, N10, and Browser observe/re-observe behavior;
- avoided broad routing keyword expansion and low-value smoke repetition.

## 0.1.0 - 2026-10-06

Initial repository version.

### Added
- software-engineering-first `webcodex-project-driver` Skill;
- short-batch execution protocol;
- explicit Session / Project / Job identity recovery rules;
- managed worktree and Git checkpoint policy;
- long-running Job and detached-process selection rules;
- independent validation/audit protocol;
- Stage closeout and retrospective protocol;
- WebCodex capability gating;
- initial architecture, capability research, experiment plan, and Stage 1 retrospective archive.

### Important constraints
- delegated CodingAgent execution is not assumed to be available;
- a ChatGPT browser window is never treated as a durable task identity;
- historical failed validation windows remain immutable evidence;
- protected/default branch merge is an explicit authorization boundary.
