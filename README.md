# NDD — notebook-driven development

<!-- Read when: orienting, or before running anything. Changes: when structure or setup changes. -->

<!-- ON CLONE: repoint this badge at your own repo (owner/name). Left as-is it opens the
     template's notebook, not yours — and you won't be able to save into it. -->
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb)

A starting point for notebook-driven development: build features in a Colab command center,
extract them to `src/` once they're settled, and keep the repo small enough to understand.

> **Using this for a project?** Hit *Use this template* on GitHub (cleaner than cloning — you
> get fresh history), tell the agent your purpose and any references, and it fills in the title,
> the line above, and `STATE.md` §1/§2/§4. Everything else works as-is.

`command_center.ipynb` is where the work happens — features are built there, in as many cells
as it takes to see them working, and moved into `src/` once they're settled. Open it in Colab,
set the config cell, run.

## Quick start

1. Click the badge above. It opens the notebook from `main` in Colab.
   First save will ask you to **Authorize googlecolab** — OAuth, no token to store.
   **Private repo?** Authorize once at colab.research.google.com/github with
   **Include Private Repos** ticked first, or Colab 404s and can't see the repo at all.
2. **One-time:** work through *Manual one-time setup* in `PLAYBOOK.md`.
3. Run the setup cell — mounts Drive, installs deps.
4. Edit the **config cell**. Every knob is there, with its alternatives and why the current
   value won. Nothing you need to change is hidden anywhere else.
5. Run top to bottom.
6. To keep your edits: the **Save in GitHub** button in the Colab toolbar. That click is the
   commit — no PR, no merge step. Details in `PLAYBOOK.md`.

## Layout

```
command_center.ipynb   the workspace — setup, config cell, features being built, output
src/<pkg>/             the archive: settled logic, one module per feature, docstring at the top
tests/                 all tests. never in a notebook cell
.gitignore             keeps data, weights, caches, outputs and credentials out of git
README.md              this file: what, how to run, what's where, how it flows
STATE.md               what's done, what's in progress, what's next
PLAYBOOK.md            Drive paths, Colab quirks, solved problems, dead ends
AGENTS.md              how agents and the user work in this repo
CLAUDE.md              points Claude Code at AGENTS.md
```

Data, weights, outputs and credentials are **not** in this repo — they live under the Drive
root set in the config cell and recorded in `PLAYBOOK.md`.

## Pipeline

<!-- input → each stage → output. one line per stage, naming the module that owns it. -->

1. **Input** — <what comes in, from where> · `src/<pkg>/<module>.py`
2. **<stage>** — <what it does> · `src/<pkg>/<module>.py`
3. **Output** — <what comes out, to where> · `src/<pkg>/<module>.py`

## Working on it

Feature lifecycle, autonomy rules and reporting format: `AGENTS.md`.
