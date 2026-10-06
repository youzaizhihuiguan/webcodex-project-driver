# Host Evaluation Results — Pre-v0.2

Date: 2026-10-07

## Scope

This records real ChatGPT/WebCodex host observations supplied after the initial Round 1 / Round 2 benchmark design. These observations are the evidence baseline for the v0.2 refactor. Do not rerun broad smoke tests merely to reconfirm them.

## Routing observations

- **T03 — cross-window registered WebCodex project:** auto-triggered.
- **T07 — durable research workflow:** auto-triggered and the resulting behavior was correct.
- **N01 — Python conceptual explanation:** correctly did not trigger.
- **N08 — software architecture discussion with no repository access:** correctly did not trigger.
- **N10 — informational WebCodex question:** triggered. This is acceptable host behavior and is not a blocker.
- **Browser workflow:** observe -> act -> re-observe behavior was correct.

## Behavior defect exposed by T03

T03 exposed one real control-plane defect:

> An ambiguous objective is not permission to invent work.

When the user requests a durable WebCodex workflow but has not supplied the actual objective, the controller must not infer a new write task from repository contents. In particular it must not autonomously create speculative:

- implementation work;
- evidence files;
- branches;
- pushes;
- or other externally visible mutations.

The correct behavior is to establish/reconcile the requested durable execution context, preserve known state, and stop at the missing objective as a decision blocker unless another authoritative project artifact already defines the exact next action.

## Routing consequence

Do not broaden the Skill description by enumerating many domain nouns such as research, browser, SSH, data, or artifacts. The current routing is already broader than static metadata inspection predicted.

v0.2 should make only an evidence-driven conceptual change:

- from a software-engineering workflow description;
- to a WebCodex durable control-plane description.

The description should continue to require a substantive WebCodex control need rather than trigger on domain vocabulary.

## Validation consequence

The v0.2 regression packet should be focused on:

1. preservation of T03/T07 positives and N01/N08 negatives;
2. no regression in Browser observe -> act -> re-observe;
3. the new ambiguous-objective non-invention rule;
4. retained Job/Session identity, provider gating, result pullback, failure-evidence, and decision-boundary behavior.

Do not spend the v0.2 cycle repeating already-proven broad smoke coverage.
