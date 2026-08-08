# PLAYBOOK

**Read when:** session start, and before re-deriving anything.
**Changes:** whenever something is learned. Append, rarely delete.

Project-specific paths, quirks, solved problems and dead ends.
If the user corrects the same thing twice, it belongs here.

## Drive layout
<!-- ON CLONE: rename the root folder after your project, here and in the notebook config
     cell. Two clones left on the same name share one Drive folder. -->
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
<!-- ON CLONE: every `vak-sah/NDD-notebook-driven-development` below is the template's repo.
     Swap in your own owner/name, or you'll be pointed at the wrong repo. -->
- Open:   the badge in `README.md`, or
          https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb
- Auth:   no key, no token. First save pops up **"Authorize googlecolab"** (OAuth) — click it.
          It can expire and re-prompt; that's normal.
          **Private repo?** The plain grant doesn't cover it — authorize once at
          colab.research.google.com/github with **Include Private Repos** ticked, or Colab
          can't see the repo at all. *Use this template* creates a private repo by default,
          so most clones need this; a public repo doesn't.
- Token:  never for opening or saving the notebook — the OAuth grant above covers that,
          private repos included. Only a **cell** that `git clone`s a private repo needs one,
          since plain git can't use the browser's session: fine-grained PAT, *Contents: read*,
          kept as a Colab Secret and read via `google.colab.userdata`. Never pasted into a
          cell, never committed.
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
- Colab `404` on `api.github.com/repos/.../contents/` means the **private-repo grant is
  missing**, not a bad branch or a missing file — GitHub returns 404, never 403, for a repo
  the token can't see, so the message points nowhere useful. Fix is *Auth* above.

## Known-bad approaches
<!-- tried, failed, don't retry -->
- `nbstripout` / pre-commit hooks to clear notebook output. They never run for Colab's
  **Save in GitHub**, which writes straight to the repo. The *Omit code cell output* setting
  in the notebook is the thing that actually works.
