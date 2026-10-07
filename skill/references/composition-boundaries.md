# Composition and Ownership Boundaries

## Ownership order

Subject to system/platform authority:

1. **Project-local explicit contract** owns frozen architecture, business rules, thresholds, acceptance definitions, risk policy, source-of-truth hierarchy, and merge/release policy.
2. **Domain Skill** owns domain-quality methods such as research methodology, statistical inference, security criteria, software architecture quality, document design, or database methodology.
3. **WebCodex Project Driver** owns WebCodex execution/control semantics.

Project Driver does not override a stricter project contract or replace domain expertise.

## Project Driver owns

- runtime/capability/provider discovery;
- exact durable identity;
- freshness/generation/fence discipline;
- authority checks for WebCodex effects;
- OBSERVE -> RECONCILE -> ACT -> VERIFY -> PERSIST/HANDOFF;
- reconcile-before-retry;
- Job/process lifecycle;
- resource ownership/lifecycle;
- Session/Goal/Agent/Task/Attempt/Wait orchestration;
- event-driven continuation readiness and recovery;
- Runner/surface placement;
- cross-surface and cross-Project control semantics;
- integration-candidate and control-plane evidence provenance;
- interruption recovery;
- evidence/result/artifact handoff;
- exact next-action persistence;
- control-plane decision boundaries.

## Domain Skills own

Examples:

- what constitutes a good research hypothesis;
- which statistical model/diagnostics are valid;
- software architecture/code-review methodology;
- security threat modeling;
- legal/financial/document-specific analysis rules;
- domain acceptance criteria when defined there.

Project Driver may persist and transport domain evidence, but must not redefine domain truth.

## Project-local instructions own

Examples:

- exact repository/source authority;
- frozen architecture;
- project-specific test or experiment gates;
- naming and release policy;
- sensitive constraints;
- protected-branch policy;
- required human approvals.

## Composition behavior

When another Skill is active:

1. keep WebCodex control-plane ownership here;
2. let the domain Skill define domain analysis/validation;
3. translate domain phases into durable WebCodex state only as needed;
4. avoid copying the domain Skill's instructions into Project Driver;
5. preserve domain evidence without reinterpreting it as control-plane truth.

## Anti-patterns

Do not:

- turn Project Driver into a router for every domain Skill;
- add domain keyword lists merely to improve routing;
- copy volatile WebCodex schemas into static references;
- force Git/worktree semantics on non-Git work;
- let a domain Skill silently override WebCodex identity/freshness contracts;
- let Project Driver invent domain work because an objective is ambiguous;
- allow two Skills to both claim authority for the same lifecycle state without an explicit precedence rule.
