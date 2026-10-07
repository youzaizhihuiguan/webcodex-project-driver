# WebCodex Capability Surface Snapshot — v0.3 Design

Date: 2026-10-07
Runtime: WebCodex 0.4.6
Build: 5072608fe74b2bfa6e8f208515c04242f475582f

## Purpose

This is historical benchmark/design evidence for the v0.3 capability-coverage decision. It is not a static API contract for the Skill.

## Live fleet

Observed:

- 2 visible Runners;
- Mac Runner online;
- Windows Runner online;
- build/protocol alignment exact/compatible;
- registered Projects online;
- Job support and broad execution/UI/runtime capabilities present.

Both observed Runners reported no configured CodingAgent provider.

## Runtime tool inventory

The live runtime reported 137 tools.

Observed runtime categories:

1. workflow
2. session
3. communication
4. goal
5. agent_task
6. agent_wait
7. coding_agent
8. project
9. runtime
10. execution
11. job
12. file
13. edit
14. git
15. cleanup
16. lsp
17. validation
18. browser
19. computer
20. artifact
21. plugin
22. skill

Additional Host/WebCodex extension gateways may be exposed outside this compact runtime category projection and must also be discovered live rather than copied into static Skill text.

## Architectural consequence

The Skill cannot stay reliable by hard-coding 137 tools.

Instead:

- tool_manifest / live inventory owns exact schemas and current recommended flows;
- runtime status owns Runner/provider/capability readiness;
- the Skill owns stable capability-family selection and orchestration policy;
- new tools inherit the generic identity/freshness/authority and observe/reconcile/act/verify/persist rules unless a new stable pattern is genuinely required.

## High-value patterns selected for v0.3

- Supervisor / workers / integrator / auditor;
- AgentTask/Attempt + AgentWait;
- event-driven Job/Agent continuation;
- multi-Runner placement;
- Browser/Computer GUI verification;
- SSH/persistent shell;
- artifact/cross-Project integration;
- Skill/Plugin/local-MCP extension;
- failure classification, automatic remediation, and escalation.

## Known capability gap

Provider-backed delegated coding is not currently executable on the observed Mac/Windows Runners because their CodingAgent provider inventories are empty.

This must remain an explicit downgrade path, not an assumed capability.
