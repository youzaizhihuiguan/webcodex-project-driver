# webcodex-project-driver

A ChatGPT Skill for using WebCodex as a durable execution/control plane for substantial stateful work across Projects, Sessions, Jobs, Goals/Tasks, Agents, Runners, surfaces, resources, evidence, and handoffs.

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

Key rules:

> uncertain outcome -> reconcile the exact prior identity before retry

> ambiguous objective != permission to invent work

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

v0.3 adds:

~~~text
Supervisor / Controller
        |
        +-- Worker(s)
        |
        +-- optional Integrator
        |
        +-- independent Auditor
~~~

plus:

- AgentTask/Attempt and AgentWait fan-out/fan-in;
- event-driven Job/Agent continuation;
- multi-Runner placement;
- Browser/Computer/SSH workflows;
- cross-Project artifact/integration pipelines;
- Runner Skill/Plugin/local-MCP extension;
- automatic safe remediation and explicit escalation boundaries.

## Current runtime caveat

The control model supports delegated Agent execution, but actual CodingAgent dispatch is capability-gated. If the active Runner has no configured provider, the controller must use Session/Job/controller execution rather than pretend a delegated worker ran.

## Ownership

Project Driver owns WebCodex control semantics:

- exact durable identity;
- freshness/fencing/generation discipline;
- runtime/capability/provider discovery;
- topology and placement;
- long-running Job/process lifecycle;
- interruption recovery;
- durable run state;
- resource lifecycle;
- evidence/result/integration handoff;
- decision boundaries.

Project-local contracts and domain Skills continue to own domain truth and methodology.

Git/worktree/checkpoint behavior remains an explicit software adaptation rather than a universal rule.

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
    autonomy-escalation.md
    validation-audit.md
    closeout-retrospective.md
    webcodex-capabilities.md
    software-git-adaptation.md
~~~

## Development policy

- Repository source is canonical.
- skill.zip is a generated release artifact.
- Non-trivial implementation happens on review branches/worktrees, not directly on main.
- Failed formal evidence is preserved.
- Runtime/provider truth comes from live WebCodex discovery.
- Broad capability coverage must not become domain-methodology duplication.
- Large low-value smoke matrices should not be rerun when equivalent real behavior has already been demonstrated.
- KeyQuant is not modified by this project.
