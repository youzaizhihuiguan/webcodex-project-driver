# ADR 0001: Scope and Source of Truth

Date: 2026-10-06
Status: Accepted

## Decision

The first version of webcodex-project-driver is software-engineering first.

It may later support research, data analysis, documents, and desktop/browser projects, but v0.1 should optimize for real Git-based software projects rather than prematurely generalizing every rule.

The GitHub repository is the canonical editable source.

Packaged `skill.zip` files are generated release artifacts.

## State authority

For software-engineering work, use the following hierarchy unless the target project defines a stricter one:

1. exact Git object/ref and workspace observation;
2. WebCodex Project / Session / Job durable identities;
3. recorded validation and runtime evidence;
4. project-owned authoritative documentation;
5. conversation text.

## Rationale

The Stage 1 experience showed that conversation-only state does not survive long tasks reliably enough. It also showed that good abstractions should emerge from observed failure modes rather than speculative generalization.

## Consequences

- v0.1 may contain Git- and validation-specific rules;
- non-software workflows should be added through separate references later;
- releases must be reproducible from repository source;
- durable IDs should appear in handoffs when they materially affect recovery.
