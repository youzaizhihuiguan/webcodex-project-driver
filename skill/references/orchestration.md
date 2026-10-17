# Orchestration

## Contents

- [Default topology](#default-topology)
- [Supervisor topology](#supervisor-topology)
- [Workflow Sessions](#workflow-sessions)
- [Durable Goal](#durable-goal)
- [Durable Agent](#durable-agent)
- [Worker contract](#worker-contract)
- [AgentTask / Attempt](#agenttask--attempt)
- [Delegated CodingAgent](#delegated-codingagent)
- [Fan-out](#fan-out)
- [Fan-in / AgentWait](#fan-in--agentwait)
- [Integrator](#integrator)
- [Auditor](#auditor)
- [Event-driven continuation](#event-driven-continuation)
- [Capability downgrade](#capability-downgrade)
- [Closeout](#closeout)

## Topology boundary

The user/project contract or `agent-operating-model` decides whether the task should use one controller, workers, an integrator, or an independent auditor.

This reference owns the WebCodex mechanics **after** that topology is justified. Do not infer topology from task size or from the mere existence of Agent/Task/Wait primitives.

## Supervisor topology

When the outer task contract calls for separated WebCodex roles, a supported topology is:

~~~text
Supervisor / Controller
        |
        +-- Worker A
        +-- Worker B
        +-- Worker C
        |
        +-- optional Integrator
        |
        +-- independent Auditor
~~~

The Supervisor owns the overall objective, durable Goal/phase, dependency graph, task admission, result reconciliation, integration gate, escalation, and user-facing report.

Workers own only their assigned bounded objective and evidence.

The Integrator is optional and is appropriate when multiple worker outputs must converge into one candidate.

When an independent audit is actually required, keep the Auditor read-only by default. It verifies the exact candidate/evidence rather than inheriting a worker's self-certification.

## Workflow Sessions

Use exact Session IDs. Do not address work by tab/window position.

For executable Session collaboration, prefer the strongest current fenced assignment/completion pattern available from the live runtime when mutation/terminal truth matters.

Session messages are coordination records, not automatic execution or wake authority.

## Durable Goal

Use a Goal for genuinely multi-step/cross-turn work when the extra durable planning state is useful.

Goal steps are durable plan markers, not proof of execution. Checkpoint only after fresh evidence supports the claimed milestone.

A Goal may correlate Sessions and AgentTasks, but that correlation does not transfer their independent authority.

## Durable Agent

Use a durable Agent identity when a controller/worker must persist independently from one ChatGPT window.

Keep Agent identity separate from:

- Endpoint generation;
- Conversation/Inbox state;
- Workflow Session;
- Goal;
- AgentTask;
- Project/Runner authority;
- execution backend.

A named Agent is not automatically an executable worker.

## Worker contract

Before dispatching a worker, define:

- exact bounded objective;
- inputs/predecessor/candidate identity;
- project/resource authority;
- expected output/result contract;
- evidence required;
- dependencies;
- integration destination;
- actions the worker must not perform.

Do not dispatch a worker with an ambiguous "continue" objective.

## AgentTask / Attempt

When durable Task execution is used:

1. create/select the exact Task;
2. assign it to the intended Agent;
3. start or recover the exact Attempt;
4. preserve Attempt freshness/fence/controller generation or equivalent live selector;
5. select one verified execution backend;
6. heartbeat only when required by the live contract;
7. reconcile backend outcome before committing Task terminal truth;
8. pull substantive results/artifacts back.

Never let a stale Attempt write terminal truth.

## Delegated CodingAgent

Before delegated execution:

1. inspect the exact Runner's current provider inventory;
2. use only an explicitly available provider/backend;
3. bind the exact Project and current context/candidate;
4. preserve idempotent/fenced run identity;
5. after uncertainty, reconcile the same CodingAgentRun instead of launching a replacement.

If no provider is configured, fall back to controller/Session/Job execution. Do not pretend delegation happened.

## Fan-out

Fan out only when units are sufficiently independent.

Each unit needs its own identity, authority, result/evidence ownership, and integration path.

Parallelism is not useful when all workers contend on the same mutable state without isolation.

## Fan-in / AgentWait

Use a durable wait when the controller should resume after exact Task terminal events.

- all semantics fit integration gates that require every selected worker.
- any semantics fit races/first-useful-result patterns.

Wait identity does not replace independent re-reading of Task results/evidence.

Do not create replacement Tasks because a waiting controller turn ended.

## Integrator

When worker outputs converge:

1. establish the exact candidate/predecessor;
2. gather verified worker outputs/artifacts;
3. resolve conflicts/dependencies;
4. produce one integration candidate;
5. run integration-level validation;
6. persist the candidate identity and evidence;
7. hand that exact candidate to the Auditor.

Worker PASS statuses alone are not an integrated PASS.

## Auditor

Use an Auditor only when independence is required by the outer contract or a concrete material risk. When used, it should independently verify:

- candidate identity;
- required evidence provenance;
- integration result;
- stale-state/fence avoidance;
- unresolved blockers;
- project/domain acceptance evidence owned elsewhere.

Keep the Auditor read-only unless a separate remediation assignment explicitly authorizes mutation.

## Event-driven continuation

Conversation/Wake/Endpoint/AgentWait primitives may support automatic continuation, but API exposure is not readiness.

Use [event-driven-continuation.md](event-driven-continuation.md) before relying on Host auto-resume.

## Capability downgrade

If a requested topology cannot execute:

- keep the same objective and durable run state;
- preserve already-started work;
- downgrade to fewer workers, Workflow Sessions, controller execution, or Jobs;
- do not invent a provider, Host wake path, or extra Runner.

## Closeout

When the outer contract closes multi-worker work:

- reconcile every required Task/Attempt/Job;
- pull back substantive results;
- complete integration if needed;
- reconcile independent audit only when required;
- checkpoint WebCodex Goal/run state when recovery needs it;
- release/handoff resources deliberately;
- preserve the exact WebCodex continuation state needed by the outer handoff.
