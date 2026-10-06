# Architecture

## Problem

A long engineering project has a lifecycle measured in hours or days. A ChatGPT model turn has a much shorter and less reliable lifecycle. Treating those two lifecycles as the same creates repeated work and ambiguous state.

The architecture therefore separates:

- **intent**: Goal / user objective;
- **execution context**: WebCodex Project and Workflow Session;
- **workspace**: checkout or managed worktree;
- **durable source state**: Git commits and refs;
- **runtime state**: Jobs, shells, remote resources;
- **validation state**: explicit evidence;
- **communication**: Session messages, assignments, Conversations;
- **delegation**: AgentTask / CodingAgentRun when available;
- **presentation**: ChatGPT window.

## Identity rule

Never infer one durable identity from another.

A ChatGPT Window is not a Workflow Session.
A Workflow Session is not a Project.
A Project is not a Git branch.
A branch name is not an exact commit.
An Agent identity is not execution authority.
A Task correlation does not grant Project access.
A message does not prove that a model turn was triggered.

Always carry the exact identifier required by the next operation.

## Control plane

Default v0.1 flow:

```text
Human objective
  |
  v
Controller model turn
  |
  +-- exact Project / Session discovery
  +-- canonical Git baseline
  +-- task decomposition
  |
  v
bounded execution batch
  |
  +-- managed worktree if writing
  +-- read / edit
  +-- focused validation
  +-- review
  +-- commit / push checkpoint
  |
  v
next short controller turn
```

Long-running work leaves the model turn:

```text
short controller turn
  -> start/reuse exact Job
  -> persist job identity / manifest
  -> yield
  -> later observe the same Job
  -> decide in a new turn
```

## Why short batches

A project should continue autonomously where safe, but a model turn should not accumulate hours of mutable state. Each batch should have one bounded objective, one validation boundary, and one recoverable checkpoint.

This is not the same as asking the user "continue?" after every task. The controller continues automatically unless a true decision boundary is reached.

## Decision boundaries

Pause for:
- frozen architecture/scope changes;
- threshold/denominator/acceptance changes;
- destructive cleanup;
- risk acceptance;
- protected/default branch merge when policy requires approval;
- missing authority or unavailable capability that materially changes the plan.

Do not pause for routine:
- worktree creation;
- focused tests;
- bounded bug fixes;
- review-branch commit/push;
- non-destructive inspection;
- continuing an already-authorized Job.

## Capability gating

Tool existence is not the same as configured availability.

Examples:
- AgentTask infrastructure may exist while no CodingAgent provider is configured;
- LSP tools may exist while pyright/gopls/rust-analyzer are unavailable;
- browser/computer capabilities vary by Runner;
- automatic continuation depends on both durable Endpoint state and an active Host carrier.

Every optional path must have a downgrade path.

## Future architecture

Once delegated providers and continuation are proven:

```text
Durable Goal
    |
Controller Agent
    |
    +-- AgentTask A -> CodingAgentRun -> worktree A
    +-- AgentTask B -> CodingAgentRun -> worktree B
    +-- Auditor Task -> read-only review
    |
 AgentWait(all)
    |
 Controller wake
    |
 checkpoint Goal / dispatch next batch
```
