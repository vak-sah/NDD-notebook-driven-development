# PLAYBOOK

**Read when:** session start, and before re-deriving anything.
**Changes:** whenever something is learned. Append, rarely delete.

Project-specific paths, quirks, solved problems and dead ends.
If the user corrects the same thing twice, it belongs here.

## Manual one-time setup
<!-- exact path, exact filename, exact format. once done, never asked again -->
<!-- Drive paths are NOT listed here — they live in the notebook config cell and nowhere
     else, so there is nothing to keep in sync. -->
- [ ] Colab: **Edit > Notebook settings > Omit code cell output when saving this notebook** —
      keeps test/run output out of the repo. Set once per notebook.
- [ ] Secrets: <Colab Secrets key name, or the Drive path> — placed by hand, never in git.
      The config cell creates the Drive folders itself; nothing to make by hand.

## Colab <-> GitHub round trip
- Open:   the badge in `README.md`, or
          https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb
- Auth:   no key, no token. First save pops up **"Authorize googlecolab"** (OAuth) — click it.
          It can expire and re-prompt; that's normal. If the repo is ever made private, go to
          colab.research.google.com/github once, tick **Include Private Repos**, authorize.
- Save:   the **"Save in GitHub to keep changes"** button (top bar) -> repo
          `vak-sah/NDD-notebook-driven-development`, branch `main`, path
          `command_center.ipynb`, write a commit message -> OK.
          That single click IS the commit. No PR, no merge step.
- Refresh after the agent changed the notebook: reopen the same link; if it looks stale,
  append `?flush_cache=true` or hard-reload.
- Save before saying `go`, so the agent starts from your latest version.

## Run / setup
- Colab bootstrap: open the badge, run top to bottom. The setup cell mounts Drive, clones the
  repo to `/content/repo` and puts `src/` on `sys.path`; the config cell makes the Drive folders.
- Test command: `pytest -q` from the repo root. Needs no Drive, no network, no GPU — same
  command in CI, a terminal, or a Colab cell.

## Reference notes
<!-- what we're taking from each reference. written once, on first read. -->
- <reference> — <what we take, what we deliberately don't>

## Conventions
- Naming:
<!-- repo layout and pipeline order live in README.md, not here -->

## Gotchas
- 

## Known-bad approaches
<!-- tried, failed, don't retry -->
- `nbstripout` / pre-commit hooks to clear notebook output. They never run for Colab's
  **Save in GitHub**, which writes straight to the repo. The *Omit code cell output* setting
  in the notebook is the thing that actually works.
