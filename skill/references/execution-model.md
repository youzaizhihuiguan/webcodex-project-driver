# Execution Model

## State ownership

Treat these as separate:
- user objective;
- WebCodex Project;
- Workflow Session;
- Git checkout/worktree;
- branch/ref/commit;
- long-running Job;
- validation evidence;
- optional Goal/AgentTask state;
- ChatGPT window.

Never silently substitute one for another.

## Takeover

When starting or resuming substantial work:

1. resolve the exact Project;
2. if an exact Session is known, resume that Session explicitly;
3. inspect Git HEAD/ref/status;
4. inspect relevant open assignments/messages;
5. inspect known active Jobs before redispatching work;
6. read recent validation/evidence and the last bounded checkpoint;
7. derive the smallest uncompleted delta.

Do not perform full-repository rediscovery by default.

## Bounded batch

A batch should normally have:
- one objective;
- known predecessor;
- limited write scope;
- explicit validation;
- a natural checkpoint.

Examples:
- fix one audited defect and its regression test;
- migrate one bounded schema change;
- implement one adapter;
- perform one read-only audit pass;
- refreeze one acceptance manifest.

## Short-turn principle

The project can run for days. The model turn should usually run only long enough to:
- decide;
- dispatch/execute one bounded unit;
- establish durable state;
- return or yield.

Do not force a long Job to share the lifetime of a single reply.

## Continue autonomously

After a batch is safely checkpointed, continue to the next authorized batch without asking "continue?" unless a project decision boundary is reached.
