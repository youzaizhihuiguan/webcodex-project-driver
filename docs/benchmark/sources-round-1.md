# Benchmark sources — Round 1

Observed: 2026-10-06.

This file records the initial source pool used to benchmark `webcodex-project-driver`. Star/install counts are point-in-time discovery signals, not quality scores.

## Standards / official guidance

### Agent Skills specification

- Repository: https://github.com/agentskills/agentskills
- Specification: https://agentskills.io/specification
- Observed GitHub stars: ~25k
- Relevant patterns:
  - standard `SKILL.md` package;
  - progressive disclosure;
  - focused references/scripts/assets;
  - validation tooling;
  - official eval guidance comparing with-Skill and baseline runs.

### Anthropic Agent Skills guidance

- Overview: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- Best practices: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
- Relevant patterns:
  - Skills compose;
  - metadata is discovery layer;
  - instructions load on trigger;
  - resources load only when needed;
  - concise context;
  - multiple evaluations and real scenarios.

### OpenAI Skill Creator

Used through ChatGPT's installed Skill Creator during this benchmark.

Relevant patterns:
- concise `SKILL.md` as control plane;
- supporting references only when useful;
- deterministic scripts for fragile repeatable operations;
- package validation before release.

## High-adoption community systems

### obra/superpowers

- https://github.com/obra/superpowers
- Observed GitHub stars: ~291k
- Relevant samples:
  - verification-before-completion;
  - writing-skills;
  - testing-skills-with-subagents;
  - subagent/worktree patterns.
- Key transferable pattern:
  - behavior Skills should be tested with baseline failure and pressure scenarios, not only read/reviewed.

### NousResearch/hermes-agent

- https://github.com/NousResearch/hermes-agent
- Observed GitHub stars: ~245k
- Relevant sample:
  - computer-use Skill.
- Key transferable patterns:
  - capture before interaction;
  - stale element-token rejection;
  - re-capture after state changes;
  - explicit tool vocabulary boundary;
  - safety escalation.

### Tencent/BrowserSkill

- https://github.com/Tencent/BrowserSkill
- Observed GitHub stars: ~7.9k in the latest search snapshot.
- Key transferable patterns:
  - explicit browser `session_id`;
  - user-tab borrow/return semantics;
  - session stop on success or failure;
  - formal human-help path;
  - host/persistence compatibility guidance;
  - verified-stage reporting rather than overstating setup completion.

### vercel-labs/agent-browser

- https://github.com/vercel-labs/agent-browser
- skills.sh observed usage: about 1M installs for `agent-browser`.
- Docs: https://agent-browser.dev/skills
- Key transferable patterns:
  - snapshot/ref interaction model;
  - stale/ref lifecycle;
  - delta snapshots for context efficiency;
  - thin discovery Skill + CLI-served instructions matching installed runtime version.

### mattpocock/skills

- https://github.com/mattpocock/skills
- High skills.sh adoption across multiple Skills.
- Relevant samples:
  - ask-matt router;
  - wayfinder;
  - diagnosing-bugs;
  - writing-great-skills;
  - implement-spec.
- Key transferable patterns:
  - router instead of monolithic Skill;
  - explicit user-invoked vs model-invoked ownership;
  - context pointers instead of duplicated state;
  - task graph/frontier;
  - real-world over-triggering is a failure mode to test.

## High-relevance orchestration / research systems

### bestagentkits/orchestrate

- https://github.com/bestagentkits/orchestrate
- Relevant because of conceptual proximity, regardless of Star count.
- Key transferable patterns:
  - live runtime discovery;
  - deterministic capability/risk routing;
  - persisted run directory;
  - attempt identity before launch;
  - reconcile uncertain work before redispatch;
  - normalized event/cursor model;
  - one authoritative reference per contract;
  - independent arbiter for higher-risk acceptance;
  - Host-specific process-supervision limits.

### pbi-agent research-lab

- https://github.com/pbi-agent/skills/tree/main/skills/research-lab
- Key transferable patterns:
  - `state.md` after every phase;
  - append-only run artifacts;
  - environment/source/assumption metadata;
  - exact handoff / next phase;
  - controller review before delegated phase completion.

### drknowhow/deep-research

- https://github.com/drknowhow/deep-research
- Key transferable patterns:
  - explicit evidence persistence;
  - runtime-agnostic orchestration contract;
  - human gates;
  - separate evidence and claim state.

## Discovery indexes

### skills.sh

- https://skills.sh/
- Used to identify high-adoption community Skills and install counts.
- Not treated as a quality authority; popularity is only one discovery signal.

## Selection rule

A source is weighted primarily by:

1. direct relevance to durable execution/control;
2. evidence of real usage;
3. clear state/lifecycle semantics;
4. failure/recovery behavior;
5. validation/eval discipline;
6. portability and explicit capability boundaries.

Star count/install count is secondary.
