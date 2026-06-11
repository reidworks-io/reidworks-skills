# One-time setup

## 1. Push to GitHub

```bash
cd reidworks-skills
git init
git add .
git commit -m "Reidworks skills marketplace: human-voice + long-run"
git branch -M main
git remote add origin git@github.com:reidworks-io/reidworks-skills.git   # <- your repo
git push -u origin main
```

## 2. Turn on GitHub Pages (the pretty site)

The site is already built in `docs/`. To publish it:

1. Repo → **Settings** → **Pages**.
2. Under **Build and deployment → Source**, pick **Deploy from a branch**.
3. Branch: **main**, folder: **/docs**. Save.
4. Wait ~1 min. Your catalog is live at `https://reidworks-io.github.io/reidworks-skills/`.

That's the whole setup — no framework, no build step. When you add a skill, edit the `skills` list near the bottom of `docs/index.html` (and the table in `README.md`), commit, and the site updates itself.

## 3. Share it

Point people at the two install commands in the README. After installing `reidworks-core`, skills trigger automatically — nobody needs to memorize names.
