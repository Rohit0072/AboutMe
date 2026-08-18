# AGENTS.md

## Cursor Cloud specific instructions

This repository is a **GitHub profile README**: the only tracked source file is
`README.md`, which GitHub renders on the profile page of the account whose
username matches the repo name. There is **no application, no build system, no
tests, no lint config, and no services** to run. The "product" is the rendered
Markdown.

Practical implications for agents working here:

- There are no dependencies to install and no lockfiles. The startup update
  script is intentionally a no-op.
- "Building/running the app" means previewing how `README.md` renders on GitHub.
  The most faithful local preview is [`grip`](https://github.com/joeyespo/grip),
  which renders through GitHub's Markdown API (requires outbound network to
  `api.github.com` / `github.githubassets.com`, which works in this environment).

### Optional: preview the README locally

`grip` is not a project dependency, so it is not part of the update script.
Install it on demand into a throwaway virtualenv (requires `python3.12-venv`):

```bash
sudo apt-get install -y python3.12-venv        # once, if venv is missing
python3 -m venv .venv-preview
.venv-preview/bin/pip install grip
# Live server (renders on each request):
.venv-preview/bin/grip README.md 0.0.0.0:6419  # open http://localhost:6419
# Or export static HTML:
.venv-preview/bin/grip README.md --export /tmp/readme_preview.html
```

`.venv-preview/` is git-ignored; do not commit it.

### Editing

Edits are plain Markdown. GitHub-flavored Markdown features (emoji shortcodes,
tables, task lists) render on GitHub even if a generic Markdown viewer differs;
use `grip` to verify GitHub-accurate output before committing.
