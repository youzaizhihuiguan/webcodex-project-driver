# webcodex-project-driver

A reusable workflow and ChatGPT Skill for running long-lived software-engineering projects through WebCodex without making the chat window the source of truth.

The project was extracted from a real multi-day Stage 1 implementation/audit/soak cycle in KeyQuant. That work exposed recurring failure modes: long model turns getting interrupted, ambiguous resume targets, duplicate work after context loss, branch/worktree drift, long-running jobs being redispatched, historical failures being overwritten, and users manually relaying information between execution and audit windows.

The repository turns those lessons into a reusable control protocol.

## Core idea

**Chat is the control surface. Durable project state lives elsewhere.**

Use:
- WebCodex Project / Workflow Session for execution context;
- Git commit + remote branch for durable engineering checkpoints;
- managed worktrees for isolation;
- Job identity for long-running execution;
- validation evidence for PASS/FAIL;
- explicit Session / Goal / Task IDs for recovery;
- short bounded model turns instead of one giant turn;
- independent audit at major gates.

Do not infer state from phrases such as "the other window", "continue the last task", or "it should still be running".

## Repository layout

```text
skill/
  SKILL.md
  agents/openai.yaml
  references/
    execution-model.md
    git-worktree-checkpoints.md
    interruption-recovery.md
    long-running-work.md
    orchestration.md
    validation-audit.md
    closeout-retrospective.md
    webcodex-capabilities.md

docs/
  architecture.md
  research/webcodex-capability-map.md
  history/stage1-lessons.md
  experiments/README.md
  decisions/0001-scope-and-source-of-truth.md

ROADMAP.md
CHANGELOG.md
```

## Current scope

v0.1 is software-engineering first. It deliberately does not assume that delegated CodingAgent providers are configured. The control model is designed to generalize later to research, data-analysis, document, and other project workflows.

## Operating model

For substantial work:

```text
Goal / user objective
  -> exact project + canonical baseline
  -> bounded task
  -> isolated worktree when writing
  -> focused validation
  -> commit + push checkpoint
  -> next bounded task
  -> independent audit at major gates
  -> long jobs tracked by exact job identity
  -> closeout + retrospective + cleanup
```

A long project may take many model turns. A single model turn should stay short enough that interruption does not destroy meaningful progress.

## Source of truth hierarchy

For engineering state, prefer:
1. exact Git commit / ref;
2. WebCodex Project / Workflow Session identity;
3. validation and runtime evidence;
4. durable Job / Goal / Task identifiers;
5. project documentation;
6. chat transcript only as explanation and coordination.

## History

See [docs/history/stage1-lessons.md](docs/history/stage1-lessons.md) for the original Stage 1 lessons and [docs/research/webcodex-capability-map.md](docs/research/webcodex-capability-map.md) for the WebCodex capability research that motivated the architecture.

## Development policy

This repository is the canonical source. Packaged `skill.zip` files are release artifacts, not the editable source of truth. Future changes should be committed with rationale and, where possible, tested on a real project before being promoted as stable behavior.
