# NDD — notebook-driven development

<!-- Read when: orienting, or before running anything. Changes: when structure or setup changes. -->

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vak-sah/NDD-notebook-driven-development/blob/main/command_center.ipynb)

A starting point for notebook-driven development: build features in a Colab command center,
extract them to `src/` once they're settled, and keep the repo small enough to understand.

> **Using this for a project?** Hit *Use this template*, open an agent session on the new repo,
> and say hello. It interviews you and makes the repo yours — see **Starting a project** below.

`command_center.ipynb` is where the work happens — features are built there, in as many cells
as it takes to see them working, and moved into `src/` once they're settled. Open it in Colab,
set the config cell, run.

## Starting a project

<!-- The agent deletes this section during onboarding — see START_HERE.md, Step 4. -->

1. **Use this template** on GitHub → *Create a new repository*. Name it after your project.
   (Not *Fork* — a fork keeps this repo's history and stays tied to it.)
2. **Open an agent session on the new repo and say hello.** That's the whole instruction.

The repo carries `START_HERE.md`, which the agent reads first. It runs a short interview — what
the project is for, what goes in and out, what done looks like, any references, which Drive
folder, any credentials — then writes your answers into `STATE.md` and `README.md`, repoints the
badge and the notebook at your repo, proposes an ordered route to MVP, and deletes itself.

You don't have to prepare anything, and nothing needs editing by hand. If you'd rather do it
yourself, `START_HERE.md` lists every file and value that changes.

Then: **Edit → Notebook settings → Omit code cell output when saving**, once, in Colab. Without
it every run's output gets committed.

## Quick start

1. Click the badge above. It opens the notebook from `main` in Colab.
   First save will ask you to **Authorize googlecolab** — OAuth, no token to store.
2. **One-time:** work through *Manual one-time setup* in `PLAYBOOK.md`.
3. Edit the **config cell** — it comes first, before anything runs. Every knob is there, with
   its alternatives and why the current value won. Nothing you can change lives anywhere else.
4. Run the setup cell — acts on that config: mounts Drive, makes the Drive folders, clones the
   repo so `src/` is importable, installs deps. It holds no settings of its own.
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
START_HERE.md          the first-session interview. deletes itself once the repo is yours
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
