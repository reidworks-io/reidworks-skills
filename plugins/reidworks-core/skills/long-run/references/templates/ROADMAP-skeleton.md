# Roadmap

The orchestrator reads this file every cycle and treats it as gospel. Each
milestone needs an `id`, dependencies, a contract (exact allowed-paths
whitelist), a DoD with verifiable bullets, and a model + subagent_type.

The lowest-numbered milestone whose deps are satisfied and which is not
already in-flight is picked next.

---

## M0 — <title>  [model: opus]  [subagent: general-purpose]  [depends: —]  [blocks: M1]

**Contract:** writes inside `path/to/scope/**`. Public API frozen except as
noted in DoD. No edits to {{areas off-limits to this worker}}.

**DoD:**
- <verifiable bullet — e.g. file `X` exists with shape `Y`>
- <verifiable bullet — e.g. coverage ≥ 90% lines on the new code>
- <tests pass: `pnpm -F <pkg> test typecheck lint build`>
- <screenshot at `.agents/screenshots/M0/`>  ← app milestones only

---

## M1 — <title>  [model: opus]  [subagent: general-purpose]  [depends: M0]

**Contract:** ...

**DoD:**
- ...

---

## Conventions

- **Allowed-paths contract is enforced post-worker.** If the worker touches
  files outside its contract, the orchestrator does NOT merge — it appends
  to `BLOCKED.md` and skips.
- **Dependency kill-tags:** if a milestone report contains `KILL`, `PIVOT`,
  or `ENVIRONMENTAL_KILL`, dependents pause until a human edits the roadmap.
- **Definition of "done":** every DoD bullet must be checkable by a
  command or a file existing. "Make it good" is not a DoD bullet.
- **Out of scope** (deferred / for human review) — list known omissions
  here so the orchestrator doesn't try to invent them.
