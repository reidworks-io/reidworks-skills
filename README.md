# Reidworks Skills

Shared, reusable skills for the whole team. One Git repo, structured as a Claude **plugin marketplace** — so the same skills work in both **Cowork** (desktop app) and **Claude Code** (CLI), and installing is one command.

## Install (everyone does this once)

In **Claude Code**:

```
/plugin marketplace add reidworks-io/reidworks-skills
/plugin install reidworks-core@reidworks-skills
```

In **Cowork**:

1. Open the **Customize** menu (gear/avatar area) and click the **Plugins** tab.
2. Under **Personal plugins**, click the **+** button and choose **Add marketplace**.
3. Pick **Add from a repository**.
4. Paste the repo path:
   ```
   reidworks-io/reidworks-skills
   ```
   (or the full URL `https://github.com/reidworks-io/reidworks-skills` — both work).
5. Cowork syncs the marketplace. You'll see **reidworks-core** listed; click **Install**, then **Authorise** when it asks about permissions.
6. The skills below now load automatically — trigger them by typing `/` in any conversation, or just describe a matching task and Claude will pick them up on its own.

> Anthropic's docs for this flow: [Use plugins in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude). Plugins you add yourself are saved to your machine, not to the org — every teammate runs these steps once.

After installing, the skills below load automatically — Claude triggers them on its own when a task matches their description. You don't need to remember command names.

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
