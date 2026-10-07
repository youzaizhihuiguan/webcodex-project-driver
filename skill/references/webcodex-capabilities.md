# WebCodex Capability Coverage

## Coverage contract

Treat the live WebCodex runtime as an extensible capability surface.

The Skill must not require a static one-to-one catalog of every current tool. Instead:

1. discover current tools/capabilities through live runtime manifests/status;
2. classify the needed capability by family, effect, lifecycle, and authority;
3. choose the smallest sufficient primitive;
4. use the exact live schema immediately before unfamiliar or version-sensitive calls;
5. apply the core identity/freshness/authority and observe/reconcile/verify rules;
6. downgrade safely when a capability is exposed but not ready;
7. treat newly added runtime tools as usable when their live contract fits an existing control pattern.

Absence from this static reference never means a live capability is unsupported.

## Capability families

### Runtime / fleet

Use for Runner health, compatibility, current capabilities, configuration, registered resources, and live tool discovery.

Prefer exact Runner targeting when placement matters.

### Project / workflow

Use for Project registration/creation, Project overview, managed worktrees, Workflow Session bootstrap, work result presentation, and task closeout.

A Project is an execution/resource boundary, not proof of the user's objective.

### Session collaboration

Use exact Workflow Sessions for durable ledgers, messages, assignment/todo state, fenced completion, handoff, and cross-window recovery.

Do not treat recent activity or a browser tab as a Session selector.

### Communication / durable Agents

Use durable Agent identity, Conversation, Inbox, Endpoint, delivery, Wake, and continuation primitives when durable controller/worker identities or Host re-entry are useful.

Agent identity alone grants no Project, filesystem, Task, or execution authority.

### Goal

Use durable Goals for substantial multi-step/cross-turn planning and progress checkpointing.

Goal completion remains a controller judgment backed by fresh evidence; the runtime cannot infer natural-language completion automatically.

### AgentTask / Attempt / AgentWait

Use for explicit worker assignment, fenced execution ownership, terminal truth, fan-out/fan-in, and event-driven rendezvous.

Keep Task identity, Attempt freshness/generation, execution backend, and Goal correlation separate.

### CodingAgent

Use delegated coding/reasoning only when a concrete provider is currently configured and authorized.

Never infer provider readiness from API exposure.

### Execution / Job / shell

Choose among sync-first process/script/shell execution, immediate async Job, detached supervisor-owned process, interactive Job input, or persistent Session shell based on form, lifetime, ownership, and restart requirements.

Duration alone does not justify detached execution.

### File / edit

Use structured search/read/edit when snapshot/revision fencing, batching, path policy, or deterministic mutation helps.

After outcome uncertainty, re-observe workspace state before another write.

### Git / cleanup

Use Git review, status, diff, commit, restore/discard, and hygiene only for Git-authoritative software workflows. Apply the software adaptation rather than making Git universal.

### LSP

Use language-server navigation/diagnostics when available. Fall back to bounded file/search inspection when unavailable.

### Build / validation

Use structured project/ecosystem validators when their provenance, diagnostics, test-count proof, dependency policy, or same-Job handoff helps. Otherwise use project-native commands with explicit evidence.

### Browser

Observe -> act -> re-observe. Treat navigation/document replacement/new snapshot as freshness boundaries. Never blindly retry an uncertain state-changing action.

### Computer

Observe the current application/window/accessibility state before control effects, then re-observe the affected state. Do not reuse stale UI assumptions across application/window changes.

### SSH / persistent remote shell

Use managed SSH resources and persistent Session shells only when remote state must persist. One-shot remote commands do not require a persistent shell.

### Artifact

Use snapshot-fenced artifact read/export/import/transfer/handoff for durable binary or cross-Project results. Verify identity/size/SHA or equivalent provenance when it matters.

### Skill / Plugin / local MCP extension

Use installed Skills, executable Skill resources, native Plugins, or authorized local MCP providers when they materially add capability.

Discover exact provider/tool/schema live. Installing/activating a Skill revision or changing Runner/provider configuration is an explicit capability-management effect, not ordinary read-only discovery.

## Exposure is not readiness

Examples:

- AgentTask APIs may exist while no CodingAgent provider is configured;
- an Endpoint API may exist while no production Host carrier can auto-resume;
- LSP may exist while no language server is installed;
- Plugin/MCP gateways may exist while no provider/tool is configured;
- Browser/Computer support may differ by Runner;
- a Project may exist on one Runner while the required platform/capability is on another.

## Downgrade safely

When an optional path is unavailable, preserve the objective and durable state, then choose a currently verified fallback.

Examples:

- no CodingAgent provider -> controller/Workflow Session/Job execution;
- no automatic continuation -> persist exact state and recover in a later turn;
- no LSP -> bounded search/read;
- no structured validator -> project/domain-native validation with explicit evidence;
- no suitable Runner -> stop at a placement/capability blocker instead of silently changing the objective;
- no Plugin/MCP provider -> continue without that extension or surface the missing capability.

Never claim an optional capability executed unless the current runtime confirms it.

## Full-surface discovery

When the task asks to exploit WebCodex broadly, use bounded live discovery to inspect:

- current tool families/categories;
- current Runner capabilities and provider inventory;
- recommended runtime flows;
- current authority/risk semantics.

Do not load full schemas for every tool preemptively. Discover the exact schema only for the next selected capability.
