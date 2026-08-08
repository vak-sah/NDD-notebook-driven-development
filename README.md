# NDD — notebook-driven development

<!-- Read when: orienting, or before running anything. Changes: when structure or setup changes. -->

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb)

A starting point for notebook-driven development: build features in a Colab command center,
extract them to `src/` once they're settled, and keep the repo small enough to understand.

> **Using this for a project?** Hit *Use this template* on GitHub — cleaner than cloning, you
> get fresh history. Then work through **Make it yours** below. Everything else runs as-is.

`command_center.ipynb` is where the work happens — features are built there, in as many cells
as it takes to see them working, and moved into `src/` once they're settled. Open it in Colab,
set the config cell, run.

## Make it yours

Four one-line edits. These are the only places in the repo that name a specific project — if
you change nothing else, a fresh clone still runs.

1. **The badge above** — swap `vak-sah/NDD-notebook-driven-development` for your own
   `owner/repo`. Left alone it opens *this* template's notebook, not yours.
2. **`command_center.ipynb` → setup cell** — the same swap, in `REPO_URL`.
3. **`command_center.ipynb` → config cell** — rename the last folder of `DRIVE_ROOT` after your
   project. Two projects both left on `NDD` share one Drive folder and overwrite each other.
4. **`PLAYBOOK.md` → *Colab <-> GitHub round trip*** — the same swap, in two places.

Then tell the agent your purpose and any references, and it fills in the title and one-liner
at the top of this file plus `STATE.md` §1. Those describe the template until you replace them.

## Quick start

1. Click the badge above. It opens the notebook from `main` in Colab.
   First save will ask you to **Authorize googlecolab** — OAuth, no token to store.
2. **One-time:** work through *Manual one-time setup* in `PLAYBOOK.md`.
3. Run the setup cell — mounts Drive, clones the repo so `src/` is importable, installs deps.
4. Edit the **config cell**. Every knob is there, with its alternatives and why the current
   value won. Nothing you need to change is hidden anywhere else.
5. Run top to bottom.
6. To keep your edits: the **Save in GitHub** button in the Colab toolbar. That click is the
   commit — no PR, no merge step. Details in `PLAYBOOK.md`.

## Layout

```
command_center.ipynb   the workspace — setup, config cell, features being built, output
src/pipeline/          the archive: settled logic, one module per feature, docstring at the top
tests/                 all tests. never in a notebook cell
pyproject.toml         pytest config only — makes src/ importable. not packaging
.github/workflows/     CI: runs the tests on every push
.gitignore             keeps data, weights, caches, outputs and credentials out of git
README.md              this file: what, how to run, what's where, how it flows
STATE.md               what's done, what's in progress, what's next
PLAYBOOK.md            Colab quirks, manual setup, solved problems, dead ends
AGENTS.md              how agents and the user work in this repo
CLAUDE.md              points Claude Code at AGENTS.md
```

Data, weights, outputs and credentials are **not** in this repo — they live under the Drive
root set in the notebook's config cell, which is the only place that path appears.

## Pipeline

<!-- input → each stage → output. one line per stage, naming the module that owns it. -->

1. **Input** — a text file under `DATA_DIR` · `src/pipeline/stub.py`
2. **Passthrough** — records through untouched; the seam a real stage replaces · `src/pipeline/stub.py`
3. **Output** — one record per line under `OUTPUTS_DIR` · `src/pipeline/stub.py`

That is a stub, not a feature: it exists so a fresh clone can prove notebook → `src/` → `tests/`
→ CI is wired up before building anything, and so the first real stage has something to replace.
Delete it once it has one.

## Working on it

Feature lifecycle, autonomy rules and reporting format: `AGENTS.md`.
