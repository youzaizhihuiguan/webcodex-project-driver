# Draft: v0.2 description candidates

Status: benchmark design only. Do not copy into production before trigger evals.

## Current production description

> Drive substantial software-engineering projects through WebCodex with durable state, managed worktrees, Git checkpoints, short bounded execution batches, validation/audit gates, long-running Job recovery, explicit Session/Goal/Task identities, and interruption-safe handoffs. Use when ChatGPT is asked to implement, refactor, audit, debug, validate, operate, or continue a multi-step codebase project through WebCodex, especially when work may span multiple model turns, worktrees, branches, long-running processes, or independent audit/execution sessions.

### Problem

This describes internal implementation details and strongly binds discovery to software terms.

False-negative risk:
- long research workflow in WebCodex;
- browser/computer workflow;
- remote long-running experiment;
- artifact handoff;
- multi-Session/Goal orchestration outside code.

It may also false-trigger on software work where WebCodex is not actually needed.

Official Agent Skills guidance recommends optimizing descriptions against realistic positive and near-miss negative queries, with the description focused on user intent rather than implementation.

---

## Candidate A — substantial WebCodex execution

> Use this skill when ChatGPT needs WebCodex to execute, continue, recover, or coordinate substantial stateful work across multiple steps or model turns. It applies to registered projects, long-running Jobs, Sessions/Goals/AgentTasks, browser or computer operation, remote execution, artifact handoffs, and interruption-safe recovery. Do not use it for ordinary conceptual answers, small one-off writing/coding tasks, or research that can be completed entirely in chat without WebCodex execution.

### Strength

Clear control-plane scope and explicit negative boundary.

### Risk

May be slightly broad because "substantial stateful work" still requires model judgment.

---

## Candidate B — durable external execution emphasis

> Use this skill when the user's task requires WebCodex as a durable external execution layer rather than a one-turn answer: managing exact project/run identities, continuing work after interruption, supervising long-running execution, coordinating multiple WebCodex contexts, or preserving evidence and handoffs across steps. Use it across software, research, browser/computer, data, and remote-operation workflows. Do not activate it merely because the prompt mentions those domains.

### Strength

Best conceptual statement of why the Skill exists.

### Risk

Some direct WebCodex tasks may not use the exact phrase "durable external execution layer" and could be missed if the model matches too literally.

---

## Candidate C — user-intent / symptom-driven

> Use this skill for substantial tasks where ChatGPT must operate through WebCodex and any of these are true: the work spans multiple steps or turns; execution may outlive the current reply; exact Session/Job/Goal/Task state matters; a browser/computer/remote resource must be controlled; prior work must be resumed or reconciled; or evidence/artifacts must survive handoff. Do not use it for simple informational, writing, coding, or research requests that do not need WebCodex stateful execution.

### Strength

Maps directly to observable user intent/symptoms instead of tool internals.

### Risk

Longest candidate and potentially higher metadata cost.

---

## Initial preference

Candidate C is the strongest **hypothesis**, not the chosen production text.

Reason:
- positive triggers are user-observable conditions;
- domain-neutral;
- explicit near-miss exclusion;
- still names WebCodex, avoiding becoming a generic "long task" Skill.

The trigger eval should decide, not preference.

## Trigger-eval method

Use the existing `trigger-evals-draft.json`.

For each candidate:
1. run every query in a fresh context;
2. run each query multiple times;
3. record whether the Skill activated;
4. compute positive recall and negative specificity;
5. preserve a validation split not used to edit the description;
6. prefer the shortest candidate that achieves comparable routing accuracy.

Do not select based on keyword coverage alone.
