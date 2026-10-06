# Experiments

This directory defines experiments that should be run before promoting optional WebCodex features into the default workflow.

## E01 - Goal recovery across windows

Purpose: verify that a durable Goal plus exact Session correlation can recover project state in a new ChatGPT window without relying on a conversation summary.

Record:
- Goal ID;
- Session ID;
- checkpoint revision;
- exact Git baseline;
- recovery steps;
- any state that still had to be reconstructed manually.

Pass condition: the new window can identify the next allowed action from durable state without broad repository reread.

## E02 - Agent Conversation Wake / Continuation

Purpose: determine whether the current ChatGPT Host can actually receive an automatic continuation from a durable Agent Wake.

Do not infer success merely because Endpoint/Continuation tools exist.

Record:
- Agent ID;
- Endpoint generation;
- Conversation ID;
- Wake ID;
- whether a new model turn was actually scheduled;
- whether manual user input was still required.

## E03 - Short-batch versus long-turn execution

Run comparable engineering work in:
- one large turn;
- several bounded batches with checkpoints.

Measure:
- interruption frequency;
- time to recover;
- duplicate reads/commands;
- uncommitted change exposure;
- user intervention count;
- final audit clarity.

## E04 - Exact Session routing

Create multiple active Sessions, post a distinct assignment to one, and test:
- generic "continue";
- explicit Session resume;
- exact assignment read.

Expected result: generic continuation is considered unsafe; exact Session identity is reliable.

## E05 - Long Job recovery

Start a long but bounded Job, end the model turn, then recover using exact `job_id`.

Pass condition:
- no duplicate dispatch;
- same Job is observed;
- terminal result is recovered;
- run manifest is sufficient.

## E06 - CodingAgent provider

Run only after a Runner advertises a configured provider.

Validate:
- Task -> Attempt -> CodingAgentRun binding;
- stale Attempt fencing;
- uncertain dispatch replay;
- terminal reconciliation;
- result handoff to Controller.

## Experiment policy

Do not promote a capability into required Skill behavior merely because the API exists. Promote it only after end-to-end behavior is observed in the actual Host/Runner environment.
