# ADR 0002: WebCodex Control Plane v0.2

Date: 2026-10-07
Status: Accepted for implementation on review branch

## Context

v0.1 proved the core recovery mechanics on real software work, but its public Skill structure still presents software/Git workflow as the universal model.

Round 1, Round 2, the draft eval suite, and the real host observations in `docs/benchmark/2026-10-07-host-eval-results.md` support a narrower change: preserve the mechanisms that already work, but move the abstraction boundary from "software engineering workflow" to "WebCodex durable control plane."

## Current structure review

### Keep

The following v0.1 behaviors are already justified by evidence and remain first-class:

- exact Project/Session/Goal/Task/Job identity where applicable;
- short bounded execution batches;
- long Job recovery without redispatch;
- capability/provider gating;
- user-visible result pullback after delegated/session work;
- immutable failure evidence;
- explicit decision boundaries;
- independent observation/verification at important gates.

### Change

The following v0.1 assumptions are too software-specific for the core:

- Git HEAD/ref/status as a universal takeover requirement;
- worktree creation as a universal write rule;
- commit/push as the universal durable checkpoint;
- software validation ordering as a cross-domain truth;
- closeout defined primarily through Git/workspace hygiene.

### Add

v0.2 needs explicit cross-domain contracts for:

- durable identity + freshness/generation proof + authority;
- OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF;
- uncertain outcome -> reconcile the same identity before retry;
- ambiguous objective != permission to invent work;
- durable run state;
- resource ownership/lifecycle;
- Project Driver versus domain Skill ownership.

## Target Skill structure

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

The structure stays intentionally small. No research/browser/SSH domain manuals are added.

## Exact migration / diff design

### `skill/SKILL.md`

- Replace the software-engineering-first description with a concise WebCodex control-plane description.
- Do not enumerate domain keywords to force routing.
- Replace Git/worktree-centric core rules with exact identity, freshness/generation proof, authority, reconcile-before-retry, ambiguous-objective non-invention, live runtime discovery, result pullback, and failure-evidence preservation.
- Replace the default software loop with OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF.
- Route Git/worktree/checkpoint rules only through the software adaptation reference.

### `skill/references/execution-model.md`

- Make the state model domain-neutral.
- Define identity/freshness/authority as separate requirements.
- Define bounded action and resource lifecycle without assuming Git.
- Keep autonomous continuation only when the objective and next action are authorized.

### `skill/references/durable-run-state.md` — new

Define the minimum recoverable cross-domain state: objective; phase/status; active work identities; evidence/result locations; resources and ownership; last verified state; exact next action; decision blockers. Do not mandate a particular storage medium.

### `skill/references/composition-boundaries.md` — new

Define ownership: platform/runtime authority; project-local explicit contract; domain Skill domain-quality methods; Project Driver WebCodex control semantics. Project Driver must not become a domain-methodology monolith or a router for every Skill.

### `skill/references/interruption-recovery.md`

- Remove Git from the universal recovery sequence.
- Make reconciliation of exact prior identities the first rule for uncertain outcomes.
- Preserve result-pullback behavior.
- Route software-specific recovery to the software adaptation.

### `skill/references/long-running-work.md`

- Keep Job/detached/shell selection by lifecycle/ownership.
- Replace the Git-shaped run manifest with generic durable run state plus optional domain extensions.
- Keep duration != detachment.

### `skill/references/orchestration.md`

- Remove worktree/Git from the default cross-domain controller definition.
- Keep exact Session/Goal/AgentTask identities and provider gating.
- Keep downgrade behavior when delegated providers are unavailable.

### `skill/references/validation-audit.md`

- Restrict Project Driver ownership to evidence identity, preservation, verification, and independent control-plane review.
- Leave domain validation method/thresholds to project-local contracts or domain Skills.
- Preserve failed formal evidence.

### `skill/references/closeout-retrospective.md`

- Generalize closeout to resources, evidence, durable run state, and exact handoff.
- Keep software Git closeout as an optional adaptation.

### `skill/references/webcodex-capabilities.md`

- Make live `tool_manifest`/runtime discovery the explicit source for volatile schemas and optional backends.
- Do not copy rapidly changing tool schemas into static Skill text.

### Git adaptation

Rename `git-worktree-checkpoints.md` -> `software-git-adaptation.md`, then state explicitly that Git/worktree/checkpoint semantics apply only when Git is an authoritative project substrate.

### Metadata/docs

- Update `skill/agents/openai.yaml` short description to control-plane wording.
- Update architecture, README, roadmap, and changelog to describe v0.2 without deleting v0.1 history.
- Record focused validation evidence.

## Routing policy

The refactor must not be justified by metadata aesthetics alone. Known host evidence says current routing already handles T03, T07, N01, and N08 correctly; N10 triggering is acceptable and is not a target for aggressive suppression. Therefore v0.2 uses a minimal metadata change and does not keyword-stuff domain examples.

## Non-goals

v0.2 does not modify KeyQuant; turn Project Driver into a universal domain Skill; statically mirror volatile WebCodex tool schemas; require Git for non-software workflows; promote Goal/Agent delegation to mandatory execution paths; merge directly to `main`; or rerun large low-value smoke suites already covered by real tests.

## Promotion gate

Promote the review branch only if focused validation shows:

1. the Skill package validates;
2. static references have no broken internal links;
3. Git/worktree semantics are no longer universal;
4. ambiguous objectives cannot authorize invented mutations;
5. exact identity, reconcile-before-retry, provider gating, result pullback, failure evidence, and decision boundaries remain present;
6. the packaged artifact is the complete Skill and is emitted as `skill.zip`.
