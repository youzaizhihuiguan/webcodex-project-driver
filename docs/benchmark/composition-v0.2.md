# Draft: Skill composition model for v0.2

Status: benchmark design only.

## Principle

`webcodex-project-driver` is a WebCodex execution/control Skill.

It should not become the owner of every domain's quality rules.

## Ownership layers

### 1. Platform/system authority

Always highest.

Includes:
- tool permissions;
- connector/runtime authority;
- host safety constraints;
- product policy;
- tool contracts.

### 2. Project-local explicit contract

Owns:
- frozen architecture;
- business rules;
- thresholds;
- acceptance definitions;
- risk policy;
- merge/release policy;
- project-specific source-of-truth hierarchy.

### 3. Domain Skill

Owns domain-quality methods.

Examples:
- research methodology;
- software architecture;
- security review;
- statistical inference;
- document design;
- database design.

### 4. WebCodex Project Driver

Owns cross-domain WebCodex execution semantics:
- runtime/capability discovery;
- durable identity;
- freshness/fencing;
- observe/act/verify;
- reconcile-before-retry;
- Job/process lifecycle;
- WebCodex resource lifecycle;
- Session/Goal/AgentTask orchestration;
- interruption recovery;
- evidence/result handoff;
- exact next-action handoff;
- control-plane closeout.

## Composition behavior

### When a domain Skill is active

Project Driver should:
1. keep control-plane ownership;
2. let the domain Skill define domain-specific analysis/validation;
3. translate domain phases into durable WebCodex execution state;
4. avoid duplicating the domain Skill's instructions;
5. preserve domain evidence without redefining domain truth.

### Example: research

Research Skill:
- hypothesis/evidence method;
- source quality;
- experiment interpretation.

Project Driver:
- Project/Session/Job identities;
- phase persistence;
- long-run recovery;
- resource lifecycle;
- exact handoff.

### Example: software engineering

Engineering Skill:
- architecture/code/testing methodology.

Project Driver:
- actual repository/worktree/Job state;
- commit/recovery checkpoints;
- WebCodex validation evidence;
- Session/audit orchestration.

### Example: browser workflow

Browser-specific Skill/runtime:
- browser command semantics;
- domain navigation workflow.

Project Driver:
- browser/page identity;
- snapshot freshness;
- durable multi-step task state;
- interruption/handoff;
- user decision boundary.

## Conflict handling

Subject to system/platform authority:

1. project-local explicit rules beat generic domain defaults;
2. domain Skill quality rules beat Project Driver domain heuristics;
3. Project Driver still controls WebCodex execution/recovery semantics;
4. no Skill may fabricate unavailable runtime capability;
5. no composition may hide failed formal evidence.

## Anti-patterns

Do not:
- copy another Skill wholesale into Project Driver;
- make Project Driver a router for every possible domain Skill;
- duplicate volatile runtime schemas;
- force software/Git semantics on non-software work;
- let a domain Skill silently override WebCodex identity/freshness contracts;
- allow two Skills to both claim ownership of the same lifecycle state.

## Router question

A separate router Skill may be useful later if the installed Skill ecosystem becomes large.

Do not add one yet.

First validate whether normal Skill discovery plus a precise Project Driver description routes correctly.
