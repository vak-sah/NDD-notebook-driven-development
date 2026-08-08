# STATE

**Read when:** first thing, every session. **Changes:** every PR.
Where this project is. Detail lives in `git log`; structure lives in `README.md`.

## 1. Goal
<!-- ON CLONE: replace this section, and clear §2 Done and §4 Next. They belong to the template. -->

**While this is the template repo:** a working NDD starting point — a Colab command center
notebook, a `src/` archive, and the five docs, such that cloning it and filling in this Goal is
enough to start a project. Done when a clone runs end to end and a first feature can be built in
the notebook and extracted without touching anything else.

References:
- <repo / site / paper / product> — <what we take from it>

## 2. Done
<!-- EVERY merged step, oldest first, numbered, one line each. complete but brief.
     scan this to spot anything missed. detail lives in git log. -->
1. `command_center.ipynb` — setup (mount Drive, clone repo, `sys.path`, deps), config cell
   (Drive root + derived paths, alternatives recorded), pipeline cell
2. Repo skeleton — `src/pipeline/`, `tests/`, `pyproject.toml` so `src/` imports without install
3. End-to-end stub — text file in, records through untouched, text file out; in `README.md`
   § Pipeline
4. CI — `pytest -q` on every push and PR
5. `README.md` § *Make it yours* — the four one-line edits that de-template a clone

## 3. In progress
<!-- at most one. branch name + where it stopped -->
- none

## 4. Next
<!-- ordered queue to MVP, one line each. re-order freely as the user redirects. -->
<!-- ON CLONE: this is your feature queue, not scaffolding. The template ships complete —
     the first item below is the first thing your project actually does. -->
1. _your first feature — replace the stub's `transform` with a real stage_

## 5. Optional / later
<!-- would step the project up, not blocking MVP -->
- none

## 6. Parked / dropped
<!-- with reason, so it isn't re-proposed -->
- none
