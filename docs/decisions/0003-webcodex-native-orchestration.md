# ADR 0003: WebCodex-Native Orchestration and Full Capability Coverage

Date: 2026-10-07
Status: Accepted for implementation on review branch

## Context

v0.2 established the generic control-plane invariants but intentionally kept advanced WebCodex orchestration minimal.

The live WebCodex 0.4.6 runtime now exposes a broad capability surface across Projects, Sessions, durable Agents, Goals, AgentTasks/Attempts, AgentWait, CodingAgent, Jobs, Runners, Browser, Computer, SSH, artifacts, validation, LSP, Skills, Plugins, and related lifecycle operations.

Copying every tool/schema into the Skill would make the Skill stale and monolithic. Ignoring these primitives would underuse WebCodex.

## Decision

Adopt two layers.

### Layer 1 — full live capability coverage

All current/future runtime tools are discoverable through live manifests/tool inventory and are eligible for use when their live contract fits the objective.

Static Skill material owns:

- capability-family selection;
- identity/freshness/authority rules;
- lifecycle/recovery rules;
- downgrade behavior;
- reusable orchestration patterns.

It does not own a frozen copy of every runtime schema.

### Layer 2 — first-class high-value patterns

Promote these cross-domain WebCodex patterns:

1. Supervisor -> Worker(s) -> optional Integrator -> independent Auditor.
2. AgentTask/Attempt + AgentWait fan-out/fan-in.
3. Event-driven Job/Agent continuation with Host readiness gating.
4. Multi-Runner placement based on authority, platform/capability, locality, lifecycle, load, and recovery cost.
5. Browser/Computer/SSH/artifact cross-surface operations.
6. Cross-Project artifact/integration pipelines.
7. Runner Skill/Plugin/local-MCP capability extension through live discovery.
8. Autonomous safe remediation with explicit escalation boundaries.

## Non-goals

- no domain methodology monolith;
- no static 137-tool catalog;
- no claim that exposed CodingAgent APIs imply a configured provider;
- no claim that Endpoint/Wake APIs imply production auto-resume;
- no automatic release/destructive authority expansion;
- no routing broadening by capability keyword stuffing.

## Current runtime evidence

At design time the connected WebCodex 0.4.6 runtime exposed 137 tools across 22 runtime categories, with Mac and Windows Runners online. Both Runners advertised broad native capabilities but no configured CodingAgent provider.

Therefore provider-backed multi-Agent execution remains a capability-gated path; the orchestration control model can be implemented now, while its provider-backed execution path requires later end-to-end validation.

## Promotion criteria

The v0.3 candidate should demonstrate mechanically that:

- all current runtime categories are represented by the dynamic coverage contract or generic fallback;
- the Skill does not statically copy volatile schemas;
- supervisor/worker/integrator/auditor roles remain distinct;
- AgentTask/Attempt/Wait semantics retain exact identity/freshness;
- multi-Runner placement is explicit;
- Browser/Computer/SSH/artifact patterns respect freshness/authority;
- safe fallback does not fabricate providers or wake readiness;
- new behavior evals cover orchestration risks;
- package contents match the candidate Skill tree.
