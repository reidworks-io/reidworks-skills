# Adding a skill

A skill is just a folder with a `SKILL.md` file. Anyone can add one.

## Steps

1. Create a folder under `plugins/reidworks-core/skills/` named in `kebab-case` (e.g. `meeting-notes`).
2. Add a `SKILL.md` (template below). Put any long reference material in a `references/` subfolder so the main file stays lean.
3. Add a row to the catalog table in the top-level `README.md`.
4. Open a pull request. Once merged, anyone gets it next time they update the marketplace.

## SKILL.md template

```markdown
---
name: your-skill-name
description: >
  One or two sharp sentences, written in the third person, describing exactly
  what this does and WHEN to use it. This is the single most important field —
  it's what Claude reads to decide whether to trigger the skill. Include concrete
  trigger phrases people would actually say.
metadata:
  category: writing             # or: eng, sales, ops...
  author: your-github-handle
---

# Your Skill Name

Brief statement of what this skill is for.

## Instructions

Write the body as directives FOR Claude, not docs for a human — e.g.
"Parse the file," not "You should parse the file." Use imperative, verb-first
steps. Keep the body under ~3,000 words; move detail into references/.
```

## What makes a skill get reused

- **A precise `description`.** Vague descriptions never trigger. Name the situation and the trigger phrases.
- **One owner.** So people know who to ask.
- **Examples.** A couple of "when this fires" examples build trust.
- **Small and sharp.** One skill that does one thing well beats a kitchen-sink skill.

## Conventions

- `kebab-case` for all folder and file names.
- Bump `version` in `plugins/reidworks-core/.claude-plugin/plugin.json` when you ship meaningful changes.
- Don't commit secrets. Use connectors/MCP for credentials.
