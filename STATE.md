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
1. _nothing yet_

## 3. In progress
<!-- at most one. branch name + where it stopped -->
- none

## 4. Next
<!-- ordered queue to MVP, one line each. re-order freely as the user redirects. -->
1. `command_center.ipynb` — setup cell (mount Drive, install deps) + empty config cell
   <!-- do this first: the README badge 404s until this file exists on main -->
2. Repo skeleton — `src/<pkg>/`, `tests/`
3. End-to-end stub — input → passthrough → output, recorded in `README.md` § Pipeline
4. CI — run tests on push
5. Prove the loop — build one throwaway feature in the notebook and extract it, to confirm
   a clone can do the same without touching anything else

## 5. Optional / later
<!-- would step the project up, not blocking MVP -->
- none

## 6. Parked / dropped
<!-- with reason, so it isn't re-proposed -->
- none
