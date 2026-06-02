# Reidworks Skills

### → Browse the catalog: **[reidworks-io.github.io/reidworks-skills](https://reidworks-io.github.io/reidworks-skills/)**

Shared, reusable skills for the whole team. One Git repo, structured as a Claude **plugin marketplace** — so the same skills work in both **Cowork** (desktop app) and **Claude Code** (CLI), and installing is one command.

## Install (everyone does this once)

### Claude Code (recommended)

```
/plugin marketplace add reidworks-io/reidworks-skills
/plugin install reidworks-core@reidworks-skills
```

One command syncs every skill in this repo. Updates land on the next `/plugin marketplace update`. Works on personal accounts.

### Cowork (personal account)

Cowork's "Add marketplace" flow is org/team-only. On a personal account you install each skill individually as a ZIP:

1. Open the latest release: **[Latest skills](https://github.com/reidworks-io/reidworks-skills/releases/tag/latest)**.
2. Download the ZIP for the skill you want (e.g. `long-run.zip`).
3. In Cowork open **Customize → Skills**.
4. Click the **+** at the top of the Skills sidebar → **+ Create skill** → **Upload a skill**.
5. Upload the ZIP. The skill appears under **Personal skills** and triggers automatically when its description matches a task.

Repeat per skill. ZIPs are auto-rebuilt on every push to `main`, so re-downloading picks up new versions.

> Refs: [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude) · [Use plugins in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude). Skills you upload are saved locally to your machine — every teammate runs these steps once per device.

### Cowork (Team or Enterprise plan)

If we ever upgrade to a Team or Enterprise workspace, the full marketplace install also works inside Cowork: **Customize → Plugins → Personal plugins → + → Add marketplace → Add from a repository →** paste `reidworks-io/reidworks-skills`. Until then, use the ZIP path above.

## Skill catalog

| Skill | What it does | When it triggers | Owner |
|-------|--------------|------------------|-------|
| **human-voice** | Edits/writes external-facing prose so it doesn't read as AI-generated. | Writing or reviewing docs, blog posts, tutorials, public READMEs, customer-facing decks, marketing copy. | mscwilson |
| **long-run** | Scaffolds a `/loop`-driven multi-agent orchestrator that builds a project end-to-end across many cycles. Requires a detailed milestone roadmap first; uses Git as the source of truth and keeps app + docs + marketing colocated. | "kick off an overnight build", "weekend run", "set up the orchestrator harness", "long autonomous build", "let Claude build this while I sleep". | johnmicahreid |

_Add a row every time you add a skill. The description column is what helps people discover it; keep it sharp._

## Repo layout

```
reidworks-skills/
├── .claude-plugin/
│   └── marketplace.json          # lists installable plugins (the catalog Claude reads)
├── README.md                     # this file — the human-browsable index
├── CONTRIBUTING.md               # how to add your own skill
└── plugins/
    └── reidworks-core/           # one plugin bundling all shared skills
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            ├── human-voice/
            │   ├── SKILL.md
            │   └── references/
            └── long-run/         # drop your skill folder here
                └── SKILL.md
```

We keep everything in **one plugin** (`reidworks-core`) so a single install gives the whole team every shared skill. If the library grows large or splits by department, we can break it into themed plugins later (`writing/`, `eng/`, `sales/`) — just add more entries to `marketplace.json`.

## Adding a skill

See [CONTRIBUTING.md](./CONTRIBUTING.md). Short version: drop your skill folder into `plugins/reidworks-core/skills/`, add a row to the catalog above, open a PR.
