# WebCodex Capability Gating

## Live runtime is authoritative for volatile contracts

Static Skill text should explain stable concepts and policy. It should not copy rapidly changing WebCodex tool schemas, provider catalogs, exact optional arguments, or current Host/Runner availability.

Before depending on a volatile capability, use the live runtime manifest/status/discovery path for the exact environment.

## Discover only what the next decision needs

Check optional capability/readiness as needed, such as:

- Projects / managed worktrees;
- Workflow Sessions and fenced assignments;
- Goals;
- durable Agents / continuation / Wake;
- AgentTask / AgentWait;
- CodingAgent providers;
- Jobs / detached processes;
- persistent SSH resources/shells;
- structured Git or validation adapters;
- LSP;
- Browser / Computer;
- Runner Skills / Plugins;
- artifact transfer.

Do not enumerate capabilities merely for completeness when they are irrelevant to the next action.

## Exposure is not readiness

Examples:

- an AgentTask API may exist while no execution provider is configured;
- LSP operations may exist while no language server is installed;
- continuation APIs may exist while no Host carrier is ready;
- a plugin gateway may exist while no provider/tool is configured;
- Browser/Computer support may differ by Runner/Host.

## Downgrade safely

When an optional path is unavailable, preserve the objective and durable state, then choose a currently verified fallback.

Examples:

- no CodingAgent provider -> controller/Session execution;
- no LSP -> bounded search/read;
- no automatic continuation -> exact Session/Job recovery on a later turn;
- no structured validator -> project/domain-native validation with explicit evidence.

Never claim an optional capability executed unless the current runtime confirms it.

## Schema freshness

When the exact call contract matters, consult the current runtime manifest immediately before using unfamiliar or version-sensitive tools. Treat remembered schemas as non-authoritative.
