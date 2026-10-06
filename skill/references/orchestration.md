# Orchestration

## v0.1 default: Session-based controller

When delegated CodingAgent providers are unavailable, orchestrate with:
- one controller;
- explicit Workflow Sessions;
- managed worktrees;
- Session assignments/messages;
- durable Git checkpoints;
- Jobs;
- independent read-only audit Sessions.

Use exact Session IDs. Do not address work by tab/window position.

## Durable Goal

Use a Goal for genuinely multi-step/cross-turn work when the runtime supports it and the added state is useful.

Goal steps are durable plan markers, not executable instructions. The controller must still verify evidence before checkpointing/completing them.

## Session assignment

For executable Session collaboration, prefer a fenced assignment pattern where available:
- create/post a todo;
- worker reads the exact assignment snapshot;
- worker completes it using the returned fence.

This is stronger than a casual message.

## Durable Agent / Conversation / Wake

These primitives may support automatic continuation, but do not assume the Host actually schedules a new model turn until tested end-to-end.

A durable message being queued is not the same as a model being awake.

## AgentTask path

If a configured execution backend is available:

```text
create AgentTask
-> assign exact Agent
-> start Attempt
-> dispatch CodingAgentRun or Endpoint continuation
-> heartbeat long Attempt when required
-> reconcile/complete exact Attempt
```

Respect Attempt fences and controller generations. Never let a stale worker write terminal truth.

## AgentWait

Use any/all waits to implement fan-out/fan-in only after the Task and continuation paths have been validated in the current environment.

## Capability downgrade

If delegated execution is unavailable, fall back to Session-based orchestration instead of pretending the task was delegated.
