# WebCodex Capability Gating

Re-discover the current runtime instead of assuming the capability set from this repository is still current.

## Capability classes

Check as needed:
- Projects / managed worktrees;
- Workflow Sessions and assignments;
- Goals;
- durable Agents / Conversation / Wake / continuation;
- AgentTask / AgentWait;
- CodingAgent providers;
- Jobs / detached processes;
- persistent SSH resources/shells;
- structured Git;
- validation adapters;
- LSP servers;
- Browser;
- Computer;
- Runner Skills;
- Runner Plugins;
- artifact transfer.

## Distinguish exposure from readiness

Examples:
- an AgentTask API may be present while `coding_agent_providers` is empty;
- LSP operations may be present while no language server is installed;
- continuation APIs may be present while no Host carrier is ready;
- plugin gateway may exist while no plugins are installed.

## Downgrade safely

Preferred fallback examples:
- no CodingAgent provider -> Session/worktree executor;
- no LSP -> bounded search/read;
- no automatic continuation -> exact Session/Job recovery on the next user/model turn;
- no structured validator for the language -> project-native commands with explicit evidence.

Never claim an optional capability executed unless the runtime actually confirms it.
