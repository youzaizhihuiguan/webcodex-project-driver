# webcodex-project-driver

A ChatGPT Skill for WebCodex-specific durable execution/control semantics across Projects, Sessions, Jobs, Goals/Tasks, Agents, Runners, surfaces, resources, evidence, and handoffs.

It is designed to compose below project-local instructions and the generic `agent-operating-model` Skill rather than acting as a general software-development or project-governance workflow.

## Core model

~~~text
durable identity
+ freshness / generation proof
+ authority
~~~

executed through:

~~~text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
~~~

Key platform rule:

> uncertain WebCodex outcome -> reconcile the exact prior identity before retry

Generic scope, proportional-rigor, material-mutation, and no-invented-gates rules live in the owning project contract / `agent-operating-model`.

## WebCodex-native coverage

The Skill does not freeze the current WebCodex API into static instructions.

Instead it:

- discovers the complete current runtime capability surface live;
- classifies capabilities by lifecycle/effect/authority;
- selects the smallest sufficient primitive;
- loads exact schemas only when needed;
- applies stable control invariants to newly added tools;
- safely downgrades when a capability/provider/Host path is not ready.

This keeps the Skill compatible with a changing WebCodex runtime while still providing opinionated orchestration behavior.

## High-value orchestration patterns

v0.3 establishes:

~~~text
Controller
        |
        +-- Worker(s), when justified
        |
        +-- optional Integrator
        |
        +-- optional Auditor, when independence is required
~~~

plus:

- AgentTask/Attempt and AgentWait fan-out/fan-in;
- event-driven Job/Agent continuation;
- multi-Runner placement;
- Browser/Computer/SSH workflows;
- cross-Project artifact/integration pipelines;
- Runner Skill/Plugin/local-MCP extension;
- automatic safe remediation and explicit escalation boundaries.

v0.3.1 operational hardening adds:

- cross-agent, Runner-local scratch lifecycle with configured Mac/Windows roots;
- stable Project/task ownership and lazy scratch creation;
- Computer/Browser/script/download staging hygiene and promote-or-delete closeout;
- durable attention routing for completion, failure, interruption, audit blockers, and user decisions.

## Current runtime caveat

The control model supports delegated Agent execution, but actual CodingAgent dispatch is capability-gated. If the active Runner has no configured provider, the controller must use Session/Job/controller execution rather than pretend a delegated worker ran.

## Ownership

Project Driver owns WebCodex control semantics:

- exact durable identity;
- freshness/fencing/generation discipline;
- runtime/capability/provider discovery;
- Task/Attempt/Wait/Job and topology mechanics;
- Runner placement;
- long-running Job/process lifecycle;
- interruption recovery of exact WebCodex state;
- resource/scratch lifecycle;
- evidence/result/integration provenance and handoff;
- Browser/Computer/SSH/artifact/cross-Project semantics.

`agent-operating-model` owns generic scope, proportional-rigor, recovery/verification, mutation-authority, and no-invented-gates guardrails when active. Project-local contracts and domain Skills own project/domain truth and methodology.

Git policy remains repository-owned. The software adaptation owns only WebCodex checkout/worktree identity, selection, reuse, recovery, and cleanup mechanics.

## Skill layout

~~~text
skill/
  SKILL.md
  agents/openai.yaml
  references/
    execution-model.md
    durable-run-state.md
    composition-boundaries.md
    interruption-recovery.md
    long-running-work.md
    orchestration.md
    runner-placement.md
    event-driven-continuation.md
    cross-surface-operations.md
    scratch-lifecycle.md
    attention-routing.md
    autonomy-escalation.md
    validation-audit.md
    closeout-retrospective.md
    webcodex-capabilities.md
    software-git-adaptation.md
~~~

## Development policy

- Repository source is canonical.
- skill.zip is a generated release artifact.
- Non-trivial implementation happens on a review branch, not directly on main; create a managed worktree only when concrete isolation/concurrency needs justify it.
- Failed formal evidence is preserved.
- Runtime/provider truth comes from live WebCodex discovery.
- Broad capability coverage must not become domain-methodology duplication.
- Large low-value smoke matrices should not be rerun when equivalent real behavior has already been demonstrated.
- KeyQuant is not modified by this project.
