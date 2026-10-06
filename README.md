# webcodex-project-driver

A ChatGPT Skill for using WebCodex as a durable control plane for substantial stateful work across multiple steps, model turns, Jobs, Sessions, resources, evidence, and handoffs.

The project originated from a real multi-day software implementation/audit cycle, then was generalized only after benchmark and host evidence showed the same control failures across non-software WebCodex workflows.

## Core model

The current v0.2 model is:

```text
durable identity
+ freshness / generation proof
+ authority
```

executed through:

```text
OBSERVE
-> RECONCILE
-> ACT
-> VERIFY
-> PERSIST / HANDOFF
```

Key rule:

> uncertain outcome -> reconcile the exact prior identity before retry

and:

> ambiguous objective != permission to invent work

## Scope

Project Driver owns WebCodex control semantics:

- exact Project/Session/Goal/Task/Job/resource identity;
- freshness/fencing/generation discipline;
- capability/provider discovery;
- long-running Job/process lifecycle;
- interruption recovery;
- durable run state;
- evidence/result handoff;
- resource lifecycle;
- decision boundaries.

Project-local contracts and domain Skills continue to own domain truth and methodology.

Git/worktree/checkpoint behavior is now an explicit software adaptation rather than a universal rule.

## Skill layout

```text
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
    validation-audit.md
    closeout-retrospective.md
    webcodex-capabilities.md
    software-git-adaptation.md
```

## Runtime freshness

Volatile WebCodex tool schemas and optional provider/backend availability are discovered from the live runtime. They are intentionally not copied into static Skill references.

## Routing policy

Routing is evidence-driven. v0.2 does not attempt to become "more general" by stuffing research/browser/SSH/data keywords into metadata.

Known host observations are recorded under `docs/benchmark/`.

## Development policy

- Repository source is canonical.
- `skill.zip` is a generated release artifact.
- Non-trivial implementation happens on review branches/worktrees, not directly on `main`.
- Failed formal evidence is preserved.
- Large low-value smoke matrices should not be rerun when equivalent real host behavior has already been demonstrated.
- KeyQuant is historical motivation only and is not modified by this project.
