# Runner Placement

## Purpose

When more than one Runner/resource can execute a bounded action, make placement explicit and recoverable.

## Placement order

Prefer these constraints in order:

1. **Authority/access** — the Runner must actually be authorized for the Project/resource/effect.
2. **Required platform/capability** — OS, architecture, Browser/Computer, local application, language/toolchain, SSH resource, provider, or other hard requirement.
3. **Project/data/resource locality** — prefer the Runner already holding the authoritative Project, data, shell, artifact, or application state when moving it would add risk.
4. **Lifecycle/restart requirement** — choose a primitive/Runner that can satisfy persistence and ownership semantics.
5. **Concurrency/load** — use current Job capacity only after hard constraints are satisfied.
6. **Recovery/integration cost** — prefer placement that minimizes fragile transfer and makes evidence easy to reconcile.

Do not optimize for idle capacity before satisfying authority and platform/locality.

## Placement record

When placement materially affects recovery, persist:

- Runner/client identity;
- Project/resource identity on that Runner;
- placement reason;
- required capability/platform;
- relevant load/concurrency observation;
- fallback Runner/path if defined.

## Cross-platform validation

For platform-sensitive software, a useful pattern is:

~~~text
integration candidate
  -> Mac validation leg
  -> Windows validation leg
  -> optional remote/other leg
  -> fan-in
  -> audit
~~~

Each leg keeps its own Job/Session/evidence identity.

Do not translate one platform's PASS into another platform's PASS.

## Moving work

Do not silently migrate mutable workspace state.

Prefer, depending on project policy:

- use the Project where it already lives;
- use a managed worktree on that Runner;
- transfer a verified artifact/candidate;
- register/create a Project only when explicitly authorized;
- use source-control refs when Git is the authoritative software substrate.

After transfer, verify the destination identity/content before execution.

## Runner failure

If a selected Runner goes offline:

1. preserve the exact prior Job/resource identity and uncertainty;
2. reconcile whether work survived or was lost;
3. determine whether another Runner can safely continue from a durable checkpoint/artifact;
4. do not start a replacement until duplicate execution risk is resolved;
5. record the new placement decision.

## Anti-patterns

Do not:

- choose a Runner only because it is "the current machine";
- assume two Runners have identical projects/files/provider configuration;
- send GUI work to a platform without the required application/surface;
- use load balancing to override data locality or authority;
- duplicate long work on another Runner merely because the first Runner stopped responding.
