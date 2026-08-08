# PLAYBOOK

**Read when:** session start, and before re-deriving anything.
**Changes:** whenever something is learned. Append, rarely delete.

Environment quirks, manual setup, solved problems and dead ends.
Not paths — those live in the notebook config cell, and only there.
If the user corrects the same thing twice, it belongs here.

## Manual one-time setup
<!-- exact path, exact filename, exact format. once done, never asked again -->
<!-- Only genuinely manual things belong here. Drive paths live in the notebook config cell;
     the config cell creates the Drive folders; CI strips notebook output. None of those are
     setup steps any more, so none of them are listed. -->
- [ ] Secrets: <Colab Secrets key name, or the Drive path> — placed by hand, never in git.

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
- _none yet_ — `<reference>` — `<what we take, what we deliberately don't>`

## Conventions
- _none yet_
<!-- repo layout and pipeline order live in README.md, not here -->

## Gotchas
- _none yet_

## Known-bad approaches
<!-- tried, failed, don't retry -->
- `nbstripout` / pre-commit hooks to clear notebook output. They never run for Colab's
  **Save in GitHub**, which writes straight to the repo and never touches a local git hook.
  Solved server-side instead: `.github/workflows/strip-notebook-output.yml` clears outputs on
  push, which is the one place that catches every save. The Colab *Omit code cell output*
  setting also works, but it has to be remembered per notebook — the workflow doesn't.
