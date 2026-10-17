# Composition and Ownership Boundaries

## Principle

Keep WebCodex control semantics below the narrowest authoritative owner of project and domain truth.

Do not invent a universal precedence hierarchy. System/platform semantics define actual instruction precedence. This reference defines **responsibility**, not host precedence.

## agent-operating-model owns

When active, `agent-operating-model` owns generic cross-cutting guardrails such as:

- authoritative-state-first behavior;
- bounded objective and no invented gates;
- proportional rigor / least machinery;
- bounded search/reuse before custom construction;
- generic uncertain-outcome discipline;
- generic diagnosis/verification discipline;
- conditional durable recovery;
- material-mutation authority;
- ownership/composition discipline.

WebCodex Project Driver must not restate those as a parallel generic workflow.

## Project-local instructions own

Examples:

- repository/source authority;
- frozen architecture and project constraints;
- validation/build commands and acceptance gates;
- Git/release/branch policy;
- sensitive project restrictions;
- current phase and exact next action.

## Domain Skills own

Examples:

- research methodology;
- statistical/scientific inference;
- software architecture/code-quality methodology;
- security threat modeling;
- legal/financial/document-specific methods;
- domain acceptance criteria.

Project Driver may carry domain evidence/results between WebCodex identities, but does not redefine domain truth.

## WebCodex Project Driver owns

- live runtime/capability/provider discovery;
- exact Project/Runner/Session/Goal/Agent/Task/Attempt/Job/resource identities;
- freshness/generation/fence/snapshot discipline;
- WebCodex effect authority;
- reconcile-before-replacement for WebCodex effects;
- Job/process/shell lifecycle;
- resource and Runner-local scratch ownership/lifecycle;
- Session/Task/Attempt/Wait/Wake mechanics;
- event-driven continuation readiness;
- Runner/surface placement;
- Browser/Computer/SSH/artifact and cross-Project control semantics;
- integration-candidate and control-plane evidence provenance;
- interruption recovery of exact WebCodex state;
- result/artifact pullback and handoff.

## Composition behavior

When multiple layers apply:

1. obtain project/domain requirements from their owning instructions/Skills;
2. let `agent-operating-model` govern generic cross-cutting behavior when active;
3. map the authorized work onto exact WebCodex identities/resources;
4. apply WebCodex freshness, reconciliation, placement, wait/wake, and lifecycle semantics here;
5. preserve domain/project evidence without reinterpreting it as control-plane truth.

## Anti-patterns

Do not:

- turn Project Driver into a generic project-management or software-engineering Skill;
- duplicate `agent-operating-model` guardrails as another mandatory checklist;
- copy domain Skill instructions into this Skill;
- copy volatile WebCodex schemas into static references;
- force Git/worktree semantics on non-Git work;
- let a domain or generic Skill overwrite exact WebCodex identity/freshness facts;
- let Project Driver manufacture project work merely because runtime objects exist.
