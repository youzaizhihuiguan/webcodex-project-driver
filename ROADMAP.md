# Roadmap

## v0.1 - durable software-engineering workflow

Goal: make long WebCodex-assisted engineering work recoverable, auditable, and resistant to chat-window interruption.

Status: initial implementation.

## v0.2 - real-project hardening

Use the Skill on at least one post-Stage-1 hardening cycle and one new project phase. Record:
- false triggers;
- overlong model turns;
- unnecessary repository rereads;
- checkpoint frequency;
- recovery accuracy;
- audit/implementation separation;
- user-visible result handoff failures.

Refine only from observed failures.

## v0.3 - durable Goal workflow

Experiment with:
- Goal admission;
- Goal checkpoints;
- exact Session correlation;
- recovery in a new chat/window;
- controller state that survives conversation truncation.

Do not promote Goal workflow to mandatory until recovery behavior is demonstrated end-to-end.

## v0.4 - Agent orchestration

When the runtime has a configured CodingAgent provider:
- durable Controller Agent;
- AgentTask + Attempt + fence;
- delegated CodingAgentRun;
- AgentWait fan-out/fan-in;
- result collection into the Controller;
- stale-attempt protection.

## v0.5 - Host continuation

Test Conversation/Inbox/Wake and Agent continuation against the actual ChatGPT host. Target:
- dispatch in one short model turn;
- background work or external event;
- durable wake;
- new short controller turn;
- no manual "continue" message.

## v1.0 - multi-project stable workflow

Requirements:
- validated across several unrelated software projects;
- interruption/recovery tested;
- long-job recovery tested;
- explicit capability downgrade paths tested;
- low false-trigger rate;
- stable repository/release process.

## Later: non-software project types

Preserve the durable-project control plane and add domain references for:
- research;
- data analysis;
- document-heavy projects;
- browser/desktop operational workflows.

Do not prematurely generalize the software-specific validation and Git rules.
