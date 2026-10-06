# WebCodex Capability Map

Research date: 2026-10-06.

This document records capabilities observed from the live WebCodex runtime used during initial design. It is descriptive, not a permanent API guarantee. Re-discover current capabilities before relying on them.

## Runtime observed

At research time:
- WebCodex version: 0.4.6;
- two online Runners: Mac and Windows;
- 137 model-visible runtime tools;
- browser and computer control available on both Runners;
- KeyQuant Python detected but no configured LSP server;
- no Runner-native plugins on the Mac;
- no CodingAgent providers advertised on either Runner.

## Capability families

### Workflow and Session
- `work_on_project`
- `finish_coding_task`
- `present_work_result`
- Session summary/handoff/closeout
- Session messages and fenced assignments

Key observation: a Workflow Session is a durable ledger, but it is not a ChatGPT window.

### Managed Projects and worktrees
WebCodex can register/create projects and create managed Git worktrees from an exact base ref. The destination is Runner-managed and registered as its own Project with a fresh Session.

This is preferable to manually inventing worktree locations for routine isolated execution.

### Goals
Durable Goal support includes:
- create/admit;
- plan steps;
- completion conditions;
- Session correlation;
- AgentTask correlation;
- checkpoints;
- lifecycle updates.

The server does not semantically evaluate natural-language completion conditions. The controller still decides whether evidence satisfies them.

### Durable Agents and Conversations
Available primitives include:
- durable Agent identity;
- Endpoint generation;
- Conversation;
- Agent inbox/delivery;
- durable Wake;
- continuation presentation.

Important: infrastructure availability does not prove that the current Host can automatically schedule a new model turn. This requires end-to-end testing.

### AgentTask / AgentWait
AgentTask provides durable task identity, assignment, leased Attempt, fence, heartbeat and terminal completion.

AgentWait can wait on exact task terminal events using any/all semantics.

These primitives solve stale-worker and ambiguous-resume problems, but delegated execution still requires a configured backend.

### CodingAgentRun
The runtime supports delegated coding runs and explicit provider selection.

At initial research time both Runners advertised no CodingAgent provider. Therefore the first Skill version must not depend on this path.

### Jobs
Execution modes are intentionally different:
- synchronous-first process/shell/script that may hand off as the same Job;
- immediate asynchronous Runner-owned Job;
- detached supervisor-owned native process for work that must survive Runner replacement.

Duration alone is not a reason to detach.

### Persistent shell / SSH
Named SSH resources and persistent Session shells can preserve remote cwd/environment/function state. This is relevant for server burn-in and operational workflows.

### Browser
Observed support:
- launch;
- targets/pages;
- semantic snapshots;
- screenshots;
- console/network diagnostics;
- admitted element actions;
- batched form interactions.

Browser control uses opaque identities and snapshot-admitted actions rather than arbitrary selectors/scripts.

### Computer
Observed support on both Mac and Windows:
- application discovery and launch;
- windows/displays;
- accessibility tree;
- keyboard/input/pointer control;
- clipboard;
- snapshots.

This creates a path to future non-code operational project workflows.

### Git
Structured operations include:
- status/log;
- bounded review;
- diff hunks;
- exact-path commit with expected HEAD.

The structured commit path is safer than indiscriminate `git add .`.

### Validation
Structured validation exists for supported ecosystems and Session validation evidence can be queried. Python projects may still need native pytest/ruff/mypy commands depending on runtime support.

### Artifacts
Capabilities include:
- host attachment -> project import;
- project artifact export/inspection;
- direct project-to-project artifact transfer;
- snapshot-fenced metadata.

### Skills and Plugins
WebCodex itself can load trusted Runner Skills and execute selected script resources without retransmitting the source through model context.

Runner-native plugin infrastructure also exists, but no plugins were installed on the researched Mac runtime.

## Design consequences

1. Discover capability before choosing an advanced path.
2. Treat exact IDs as control-plane state.
3. Do not equate tool exposure with configured provider availability.
4. Prefer native durable identities over chat-memory reconstruction.
5. Keep fallbacks explicit.
6. Test continuation and delegated-agent paths independently before making them default.
