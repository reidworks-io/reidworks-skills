---
name: long-run
description: >
  Set up a long-running multi-agent orchestrator that builds a project end-to-end across many
  /loop cycles. Use when the user wants to "kick off an overnight build", "start a weekend run",
  "set up the orchestrator harness", "run a long autonomous build", or any task framed as "let
  Claude build this while I sleep". Hard-requires a detailed milestone roadmap before kickoff —
  if the user lacks one, this skill stops and routes them to write one (it does NOT auto-generate
  the roadmap). Uses Git as the source of truth; expects the app, docs, marketing site, tests,
  and screenshots to live in the same repo so the prototype's assets evolve together. Do NOT
  apply to short one-shot tasks, single PRs, or anything that can finish in one Claude turn.
metadata:
  category: eng
  author: johnmicahreid
---

# Long Run — autonomous multi-agent build orchestrator

Distilled from a working pattern (weekend SDK + monorepo build, 14+ milestones, file-based
state, `/loop`-driven). Build the harness; the user owns the kickoff.

## Operating model

- **One orchestrator, many workers.** A `/loop` cycle re-fires every N minutes. Each cycle the
  orchestrator picks the next eligible milestone, spawns a worker via the Agent tool, runs
  gates, merges (or files a block), updates state, exits the turn.
- **State on disk, not in conversation.** Everything that matters across cycles lives in
  `.agents/STATE.md`, `.agents/DIGEST.md`, `.agents/BLOCKED.md`. The orchestrator is stateless
  between cycles and reconstructs from these files every time.
- **Git is the source of truth.** Workers branch, commit, open PRs, squash-merge. The diff is
  the artifact. No deployments, no force pushes.
- **Roadmap is gospel.** Never invent milestones; only execute them.
- **One repo, one prototype.** App, docs, marketing, tests, screenshots all colocated so a
  single PR can update related surfaces atomically.

## Hard prerequisites

Do not proceed to scaffolding until ALL are true. If any is missing, engage the user.

1. **Git repository.** `test -d .git`.
2. **Detailed roadmap** at `.agents/ROADMAP.md` (or equivalent) with explicit per-milestone:
   - `id` (e.g. `M0`, `P2.1`)
   - dependencies (other milestone ids)
   - contract (exact allowed-paths whitelist)
   - DoD (verifiable bullets, not "make it good")
   - model + subagent type
3. **Source-of-truth docs in repo** for the surfaces in scope:
   - `DESIGN.md` if UI work is in scope
   - `VOICE.md` if user-facing copy is in scope
   - architecture doc if SDK/library work is in scope
4. **Quality gates wired up.** A single command that runs typecheck + lint + test + build.
   Workers must pass it before merge.
5. **Deny-list** in `.claude/settings.local.json` blocking deploy commands and force-push.
6. **`.agents/STOP`** convention as kill switch.

## Phase 1 — Pre-flight audit

Run the audit. Report each as ✓ or ✗.

```bash
echo "--- long-run pre-flight ---"
test -d .git && echo "✓ git repo" || echo "✗ not a git repo"
git remote -v | grep -q . && echo "✓ git remote configured" || echo "⚠ no git remote (PR flow falls back to local squash-merge)"
for f in .agents/ROADMAP.md .agents/orchestrator-prompt.md .agents/STATE.md .agents/DIGEST.md .agents/BLOCKED.md; do
  test -f "$f" && echo "✓ $f" || echo "✗ $f"
done
test -f .claude/settings.local.json && grep -q '"deny"' .claude/settings.local.json && echo "✓ deny list" || echo "✗ no deny list"
test -f DESIGN.md && echo "• DESIGN.md present" || echo "• DESIGN.md absent (required if UI in scope)"
test -f VOICE.md && echo "• VOICE.md present" || echo "• VOICE.md absent (required if copy in scope)"
```

If the audit fails on git, stop entirely. If it fails only on harness files, that's expected —
Phase 3 scaffolds them. If the roadmap is missing, jump to Phase 2.

## Phase 2 — Roadmap engagement (only if missing or incomplete)

**Do not auto-generate the roadmap.** It encodes the user's product decisions and the orchestrator
treats it as gospel — generating it without user buy-in poisons the entire run.

Ask the user:

> A long-running orchestrator needs a detailed milestone plan before kickoff. What do you have?
> - A) I have a roadmap doc — let me point you at it
> - B) I have a high-level idea but no milestone plan
> - C) I haven't thought through the project yet

**If A:** ask the path, read it, audit against the per-milestone schema (id, deps, contract,
DoD, model). For each missing field, ask the user to fill it in OR offer to draft a candidate
they review. Do not silently fill gaps.

**If B or C:** stop the skill. Tell the user:

> A long-running build needs an approved spec. Brainstorm the problem first (e.g. via
> `/office-hours` or your team's equivalent), then lock in architecture (e.g. via
> `/plan-eng-review`), then come back. Generating a plan unprompted would burn cycles on
> the wrong work — that call belongs upstream.

When extending a partial spec into per-milestone contracts, for each milestone confirm:

- id + human title
- dependencies (which milestones must finish first)
- allowed-paths whitelist — exact globs the worker may touch (drives the contract-violation check)
- DoD bullets — verifiable, concrete (tests pass, file exists, screenshot committed, coverage ≥ N%)
- which surfaces this touches (sdk / app / docs / marketing) — drives colocation expectations
- model + subagent_type

Rule of thumb: if a one-line shell test cannot verify the DoD, it's not concrete enough.

## Phase 3 — Scaffold the harness (only after the roadmap is locked)

Read the templates bundled with this skill at `references/templates/` and write them into the
repo, substituting `{{placeholders}}` interactively:

- `references/templates/orchestrator-prompt.md` → `.agents/orchestrator-prompt.md`
- `references/templates/STATE.md` → `.agents/STATE.md`
- `references/templates/DIGEST.md` → `.agents/DIGEST.md`
- `references/templates/BLOCKED.md` → `.agents/BLOCKED.md`
- `references/templates/settings.local.json` → `.claude/settings.local.json` (merge if exists)
- `references/templates/ROADMAP-skeleton.md` → starting point if the user is hand-authoring

Required substitutions in the orchestrator prompt (ask the user, don't guess):

- `{{project-name}}`
- `{{gate-command}}` — single shell command that runs typecheck + lint + test + build for the
  whole project (e.g. `pnpm turbo run typecheck lint test build --concurrency=1`)
- `{{source-of-truth-docs}}` — list of docs the orchestrator reads each cycle (DESIGN.md,
  VOICE.md, architecture doc, etc.)
- `{{merge-strategy}}` — `gh pr create + gh pr merge --squash` (default, requires remote) OR
  `local squash-merge to main` (no remote)
- `{{notification-block}}` — paste the Slack block from `references/templates/notify-slack.md`
  if the user wants notifications; otherwise replace with "skip notification".
- `{{rate-limit-policy}}` — default is "write to BLOCKED.md, end turn, next /loop fire retries"

Add to `.gitignore`:

```
.agents/STOP
```

Commit the harness:

```bash
git add .agents/ .claude/settings.local.json .gitignore
git commit -m "chore: scaffold long-run orchestrator harness"
```

## Phase 4 — Asset colocation check

The prototype's app, docs, marketing, tests, and screenshots must live in this repo so they
evolve together. Audit the layout:

```bash
ls -d apps/* packages/* docs/ marketing/ 2>/dev/null
find . -maxdepth 3 -name 'DESIGN.md' -o -name 'VOICE.md' -o -name '*-architecture.md' 2>/dev/null | grep -v node_modules
```

Common shapes that work:

- **Monorepo (SDK + apps):** `packages/<lib>/`, `apps/<app>/`, top-level `DESIGN.md` /
  `VOICE.md` / architecture doc, `.agents/screenshots/<milestone>/`.
- **Single app:** `src/`, `docs/`, optional `marketing/`, `tests/`, `.agents/screenshots/<milestone>/`.

If the user keeps assets elsewhere (Notion docs, Webflow marketing, Figma-only design), flag this:

> The orchestrator can only update files in this repo. {{asset}} lives outside it, so the build
> can't keep it in sync. Bring it into the repo (even as a stub) or accept that {{asset}}
> will drift.

## Phase 5 — Safety rails

Walk through each. Confirm before kickoff.

1. **Third-party API spend caps.** Any runtime API key used by the demo (Anthropic, OpenAI,
   etc.) should be a dedicated key with a hard workspace spend cap. Workers cannot exceed
   what the key allows.
2. **Pre-push hook** at `.git/hooks/pre-push` running the full gate command. Optional but
   recommended — catches regressions before they hit the remote.
3. **Mac wake-lock.** In a separate terminal: `caffeinate -dimsu &`. If the machine sleeps,
   `/loop` dies silently and hours of cycles are lost. **Do not swap `/loop` for `launchd`,
   `cron`, or a remote routine "for resilience"** — you lose live visibility and headless
   `claude -p` has known toolchain traps (see Known traps #1, #4).
4. **Kill switch test.**
   ```bash
   touch .agents/STOP && ls .agents/STOP && rm .agents/STOP
   ```
5. **Notification channel** (if configured) — confirm the orchestrator can reach it before kickoff.

## Phase 6 — Kickoff

Tell the user — do not run this yourself:

```
/loop 45m act as the orchestrator per .agents/orchestrator-prompt.md
```

Default interval: **45 minutes** (balances Anthropic rate-limit recovery against forward
progress). 60 minutes is also fine for smaller cycles. Avoid <30 minutes — rate windows get
squeezed.

Final words to the user:

- Walk away. Check back periodically via `STATE.md` and `DIGEST.md`.
- To stop early: `touch .agents/STOP`. Resume with `rm .agents/STOP` then re-issue the /loop command.
- Read order on return: `BLOCKED.md` → `DIGEST.md` → recent PRs → `STATE.md`.

## Hard rules for this skill

- **Never invoke /loop yourself.** This skill builds the harness; the user kicks off.
- **Never auto-generate the roadmap.** If missing, route the user upstream and stop.
- **Never commit without showing the user the harness files first.** They are about to delegate
  authority to an orchestrator — they need to see what it will do.
- **Never push to main from this skill.** All commits are local; the user pushes manually.

## Known traps (from real runs)

Each of these cost time on a real autonomous build. The templates this skill
ships now encode the fix; the explanations live here so future maintainers know
why the templates look the way they do.

### Trap 1 — Headless orchestrator hides its work

**What goes wrong:** Setting up the orchestrator via `launchd`, `cron`, or a
remote routine "for resilience" sounds smart, but `claude -p` running
non-interactively writes nothing useful to stdout / stderr. The only live view
is the JSONL session log under `~/.claude/projects/<repo>/`, which is awkward
to follow with `jq` and easy to miss when a worker turn goes sideways. You can't
catch a bad turn until after it lands on `main`.

**The fix:** Run the orchestrator in an *attended* `/loop` in your interactive
terminal. Use `caffeinate` for the wake-lock. Accept that if the session dies
(laptop sleeps without caffeinate, terminal closes), the cycle dies — that's the
trade. The visibility is worth it.

**If you genuinely need unattended overnight:** wrap `claude -p` in `launchd`,
but verify the MCP toolchain works headless first (Trap 4) and accept that
you'll be reading `DIGEST.md` + JSONL after the fact rather than watching live.

### Trap 2 — Bookkeeping carried across cycles

**What goes wrong:** Cycle N updates `STATE.md` or `DIGEST.md` but doesn't commit
before spawning the worker. Cycle N+1 inherits the dirty working tree. A
`git stash` somewhere — to give the worker a clean checkout — drops uncommitted
bookkeeping into a dangling stash. Hours later, "where did cycle 19's `DIGEST`
entry go?" becomes real archeology.

**The fix:** The `orchestrator-prompt.md` template now requires the orchestrator
to **commit `STATE.md` / `DIGEST.md` atomically at every meaningful checkpoint**
(dispatch, worker return, gates pass, block), not at end-of-cycle. This makes
recovery from a crashed cycle trivial: the next cycle just reads the committed
state. Push them directly to `main` as `chore: orchestrator cycle N — <outcome>`
(see Trap 5 — the "never push to main" rule is carved out for bookkeeping).

### Trap 3 — BLOCKED entries without a decision tree

**What goes wrong:** A worker reports an issue, the orchestrator dumps a
paragraph to `BLOCKED.md`, the cycle ends. When the human comes back —
potentially days later — they have to re-derive: what specifically failed,
what was already tried, what are the realistic options, what does each cost?
Context decay turns a 10-minute decision into an afternoon.

**The fix:** The `BLOCKED.md` template now requires every entry to carry four
parts: **symptom** (exact failure), **what was tried** (one attempted fix and
why it didn't work), **options forward** (2–3 paths with cost / risk /
reversibility), and **recommended path** (the orchestrator's pick + reasoning).
If the orchestrator can't fill all four, the entry should say so explicitly —
that itself is information.

### Trap 4 — Headless MCP tool surprises

**What goes wrong:** Interactive Claude sessions auto-resolve a wide range of
MCP tools (Slack, Linear, Notion, etc.). `claude -p` in headless / `launchd` /
remote-routine contexts often ships with a narrower default toolset; deferred
MCP tools need an explicit `ToolSearch` round-trip to load. A Slack
notification step that "works in dev" silently no-ops in production.

**The fix:** If notifications matter, test them from a *non-interactive* Claude
session (`claude -p "use the Slack MCP to send a test message"`) before
kickoff. The `notify-slack.md` template now flags this. If the headless path
doesn't load the tool, either add an explicit `ToolSearch` step to the
orchestrator-prompt or treat `DIGEST.md` as the only reliable heartbeat and
drop the notification.

### Trap 5 — "Never push to main" is too broad

**What goes wrong:** A blanket "never push to main" rule is correct for
milestone code (which flows through PR + squash merge) but wrong for
orchestrator bookkeeping. `STATE.md` and `DIGEST.md` updates fire every cycle;
routing them through PRs is bureaucratic theater, and not pushing them means
cross-machine continuity breaks.

**The fix:** The `orchestrator-prompt.md` template now carves out an exception:
> Never push *code* to `main`. `STATE.md`, `DIGEST.md`, and `BLOCKED.md` updates
> may be pushed directly to `main` as `chore: orchestrator cycle N — <outcome>`.

---

## Completion

Report status using one of:

- **DONE** — harness scaffolded, roadmap locked, safety rails confirmed, kickoff command in the user's hands.
- **DONE_WITH_CONCERNS** — kickoff is possible but specific risks were flagged (list them).
- **BLOCKED** — missing roadmap, no git, or a fundamental gap that needs human work first.
- **NEEDS_CONTEXT** — waiting on user input.
