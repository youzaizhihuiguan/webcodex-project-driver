# Event-Driven Continuation

## Purpose

Use durable waits/wakes when work should continue after a Job/Task event without keeping one model turn alive.

## Readiness rule

API exposure is not automatic-continuation readiness.

Before relying on Host re-entry, verify the current live contract and readiness. For durable Agents, treat the runtime's production auto-resume/readiness signal for the exact Agent/Endpoint generation as authoritative when available.

An Endpoint is not Project authority, and a Wake is not Task completion evidence.

## Durable Agent continuation

Typical lifecycle:

~~~text
durable Agent
-> current Endpoint generation
-> present/establish supported Host continuation
-> durable Wake/event
-> fresh model turn
-> bootstrap exact Agent/Endpoint generation
-> consume/reconcile the exact Wake
-> continue
~~~

Rotating an Endpoint makes older generations stale. Never resume using a remembered old generation after rotation.

## AgentTask fan-in

For multiple exact AgentTasks:

- use all-wait semantics when every source is required;
- use any-wait semantics when first useful/terminal source should resume the controller;
- keep exact Task identities and optional Goal correlation;
- after wake, independently re-read the Goal/Tasks/results;
- do not treat wait delivery as result content.

If a selected source is already terminal and the live wait contract rejects that state, reconcile it directly rather than manufacturing a new Task.

## Job terminal attention

When only an existing Job terminal transition blocks progress:

- retain the exact Job identity;
- arm/reuse the supported terminal wait/continuation;
- end/yield the current turn if the Host continuation contract requires it;
- on re-entry, observe the same Job.

Do not redispatch the command merely because the prior turn ended.

## When continuation is unavailable

If no production wake-capable Host path is ready:

1. preserve exact Session/Goal/Task/Job identities;
2. persist the last verified state;
3. record the exact next observation/action;
4. stop cleanly;
5. recover those same identities in the next user/model turn.

This is a valid downgrade, not a failure of the durable workflow.

## Avoid polling loops

Do not consume an entire model turn repeatedly polling a long Job/Task when a durable wait is available.

Polling remains appropriate for short bounded readiness inside the current turn when the live contract explicitly supports it.

## Wake safety

On wake/re-entry:

- verify exact Agent/Endpoint generation;
- reconcile source Task/Job state;
- consume/acknowledge the exact continuation only as required by the live contract;
- preserve result/evidence provenance;
- continue only the authorized unfinished delta.
