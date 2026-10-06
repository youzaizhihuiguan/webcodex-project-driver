# Orchestration

## Default controller

Use one controller with explicit durable identities. Add Sessions, Goals, AgentTasks, Jobs, resources, or independent audit contexts only when they materially help the objective.

Do not require Git/worktrees merely because orchestration is multi-step.

## Workflow Sessions

Use exact Session IDs. Do not address work by tab/window position.

For executable Session collaboration, prefer the strongest current fenced assignment/completion pattern available from the live runtime rather than casual messages when mutation/terminal truth matters.

## Durable Goal

Use a Goal for genuinely multi-step/cross-turn work when the runtime supports it and the extra durable planning state is useful.

Goal steps are durable plan markers, not proof of execution. Verify evidence before checkpointing/completing them.

## AgentTask / delegated execution

Before delegation:

1. discover current provider/backend readiness;
2. create/address the exact Task/Attempt identities required by the live contract;
3. preserve attempt fence/controller generation or equivalent freshness proof;
4. dispatch only through a confirmed available backend;
5. reconcile terminal state before accepting worker claims;
6. pull substantive results back into the controller/user response.

Never let a stale worker write terminal truth.

## Durable Agent / continuation / waits

Conversation/Wake/Endpoint/AgentWait primitives may support automatic continuation, but an API being exposed does not prove the Host will schedule a fresh model turn.

Use these only after current Host/Runner readiness is observed.

## Capability downgrade

If delegated execution is unavailable:

- keep the same objective and durable run state;
- fall back to controller/Workflow Session/Job execution or another currently available path;
- do not pretend delegation occurred;
- do not invent a provider or backend because the API exists.

## Fan-out / fan-in

Use multiple workers only when the work can be separated with clear identity, authority, evidence ownership, and result reconciliation. Keep auditors read-only by default when independence matters.
