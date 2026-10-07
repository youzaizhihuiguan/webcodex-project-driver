# v0.2 evaluation plan

Status: v0.2 is implemented on `review/v0.2-control-plane`; focused Host regressions are recorded in `2026-10-07-host-eval-results.md`; this document remains the evaluation contract used for promotion review.

The original plan predates implementation. Keep the routing and behavior criteria below as the evaluation contract; use the recorded Host evidence plus focused repository/package checks for the current review candidate rather than treating this document as evidence that the Skill is still unchanged.

## Two separate test layers

### Layer A — trigger routing

Question:

> Does the Skill activate when WebCodex control is needed, and stay out of the way when it is not?

Input:
- `trigger-evals-draft.json`;
- current production description;
- description candidates A/B/C.

Method:
- clean context per query;
- multiple runs per query where the Host permits;
- positive and negative trigger rate;
- train/validation split;
- do not optimize against the validation queries.

Metrics:
- positive recall;
- negative specificity;
- false-positive count;
- false-negative count;
- metadata length.

### Layer B — behavior

Question:

> Once active, does the Skill make better WebCodex control decisions?

Input:
- `behavior-evals-draft.json`.

Configurations:
1. current Skill baseline;
2. v0.2 candidate.

For suitable cases, a no-Skill baseline may also be informative.

Metrics:
- assertion pass rate;
- duplicated execution count;
- wrong-identity incidents;
- stale-handle incidents;
- fabricated-capability incidents;
- recovery steps;
- token/time overhead where the Host exposes it.

## Mechanical versus judgment assertions

Use mechanical checks when possible.

Examples:
- exact Session id used before mutation;
- same Job id observed rather than a new Job launched;
- provider list checked before CodingAgent dispatch;
- Browser snapshot obtained after navigation;
- JSON/run-manifest fields exist;
- changed paths exclude unrelated files.

Use human/LLM judgment for:
- whether the chosen durable scope was appropriate;
- whether a user decision boundary was correctly identified;
- whether composition respected domain ownership.

## Current Host limitation

Trigger activation is a ChatGPT/Work Host behavior. A single already-running conversation cannot honestly simulate fresh Skill discovery for twenty independent prompts.

Therefore:
- do not label trigger evals PASS merely by reading the descriptions;
- run them in fresh Work conversations/sessions or an available Skill-eval harness;
- preserve the transcripts/activation evidence.

Behavior cases that depend on real WebCodex state should similarly use controlled fixtures or dedicated Sessions/Jobs rather than invented logs.

## Promotion gate for v0.2

Promote only if:

1. routing is at least as precise as the current version for software cases;
2. non-software WebCodex positives trigger reliably;
3. near-miss negatives remain mostly inactive;
4. behavior evals improve or preserve all critical recovery/fencing cases;
5. token/time overhead is acceptable;
6. no project-specific KeyQuant rule leaks into the generic core.

## First practical run

Recommended first manual trigger batch:
- T03: generic cross-turn WebCodex project;
- T04: Browser workflow;
- T07: research workflow;
- N01: conceptual Python;
- N08: architecture-only software request;
- N10: informational WebCodex question.

These six cases quickly reveal whether the description is too narrow or too broad before paying for the full matrix.
