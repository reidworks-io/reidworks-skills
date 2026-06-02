# Blocked / Open Decisions

Items the orchestrator refused to guess at, or that need a human call.
**Read first when you come back.**

## Required entry format

Every entry the orchestrator writes must include all four sections. If a
section can't be filled, say so explicitly — that absence is the signal.

```
## §N. <milestone-id> — <one-line summary> (cycle K, <date>)

**Symptom.** Exact failure: test name, error message, file:line, gate that
failed, contract path that was violated. Quote the worker's output for the
key lines so a returning human doesn't have to re-derive context.

**What was tried.** At least one attempted fix and why it didn't work. If
no fix was attempted (e.g. contract violation, environmental kill), state
that and why a retry wasn't appropriate.

**Options forward.** 2–3 realistic paths. For each: (a) what changes,
(b) estimated effort, (c) risk / reversibility, (d) what it doesn't fix.

**Recommended path.** The orchestrator's pick and the one-sentence reason.
If no recommendation is possible without more context, name the specific
question a human needs to answer first.
```

Append new entries; never mutate prior ones.

---

## Pre-existing (set before the autonomous run)

_List known unknowns here before kickoff — naming decisions, vertical positioning,
API keys still to provision, taste calls the orchestrator should not make._

---

## Raised during autonomous run

_The orchestrator appends entries here when it hits a fork it cannot resolve,
a gate it cannot pass, or a contract violation it cannot merge._
