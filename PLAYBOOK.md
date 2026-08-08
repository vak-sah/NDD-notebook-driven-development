# PLAYBOOK

**Read when:** session start, and before re-deriving anything.
**Changes:** whenever something is learned. Append, rarely delete.

Project-specific paths, quirks, solved problems and dead ends.
If the user corrects the same thing twice, it belongs here.

## Drive layout
- Drive root: `/content/drive/MyDrive/NDD/`   <- set once in the notebook config cell
- Data:       `<root>/data/`
- Outputs:    `<root>/outputs/`
- Secrets:    <Colab Secrets key name, or `<root>/secrets/<file>`>

## Manual one-time setup
<!-- exact path, exact filename, exact format. once done, never asked again -->
- [ ] Colab: **Edit > Notebook settings > Omit code cell output when saving this notebook** —
      keeps test/run output out of the repo. Set once per notebook.
- [ ] Create the Drive root above and place any secret file there by hand.

## Colab <-> GitHub round trip
- Open:   the badge in `README.md`, or
          https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb
- Auth:   no key, no token. First save pops up **"Authorize googlecolab"** (OAuth) — click it.
          It can expire and re-prompt; that's normal.
          **If the repo is private, the plain grant is not enough** — go to
          colab.research.google.com/github once, tick **Include Private Repos**, authorize.
          Do this before anything else; without it Colab can't see the repo at all.
          *Use this template* defaults the new repo to private, so a fresh clone normally
          needs this step. Making the repo public removes the need for it entirely.
- Save:   the **"Save in GitHub to keep changes"** button (top bar) -> repo
          `vak-sah/NDD-notebook-driven-development`, branch `main`, path
          `command_center.ipynb`, write a commit message -> OK.
          That single click IS the commit. No PR, no merge step.
- Refresh after the agent changed the notebook: reopen the same link; if it looks stale,
  append `?flush_cache=true` or hard-reload.
- Save before saying `go`, so the agent starts from your latest version.

## Run / setup
- Colab bootstrap:
- Test command:

## Reference notes
<!-- what we're taking from each reference. written once, on first read. -->
- <reference> — <what we take, what we deliberately don't>

## Conventions
- Naming:
<!-- repo layout and pipeline order live in README.md, not here -->

## Gotchas
- **Colab `404 Not Found` on `api.github.com/repos/.../contents/?ref=main`** — this is the
  private-repo grant missing, not a broken branch or a missing file. GitHub answers 404 (never
  403) for a private repo the token can't see, so the message is misleading. Fix: tick
  **Include Private Repos** at colab.research.google.com/github (see *Auth* above). Verified:
  with an authorized token the same call returns the repo root fine. Expect this on every
  private clone of the template, including the first run of a brand-new one.
- The Colab badge / `blob/main/command_center.ipynb` link 404s until that notebook exists on
  `main` — a *different* 404 from the one above, and the reason it's `STATE.md` §4 item 1.

## Known-bad approaches
<!-- tried, failed, don't retry -->
- `nbstripout` / pre-commit hooks to clear notebook output. They never run for Colab's
  **Save in GitHub**, which writes straight to the repo. The *Omit code cell output* setting
  in the notebook is the thing that actually works.
