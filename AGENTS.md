# AGENTS.md — operating contract

**Read when:** every session, before anything else. **Changes:** rarely.
A chat instruction beats this file for that turn only. Don't silently rewrite it.

---

## 0. Doc map — what is written where

| File | Answers | Changes |
|---|---|---|
| `START_HERE.md` | The first-session interview that makes a fresh copy specific. Deletes itself | Never — it's gone after one use |
| `README.md` | What is this, how do I run it, where does everything live, how does the pipeline flow | When structure or setup changes |
| `AGENTS.md` | How we work (this file) | Rarely |
| `CLAUDE.md` | Nothing of its own — imports `AGENTS.md` for Claude Code | Never |
| `STATE.md` | What's done, what's now, what's next | When the project moves — a step lands, is parked or reordered |
| `PLAYBOOK.md` | Environment quirks, manual setup, solved problems, dead ends | When something is learned |
| docstrings | What this specific feature does and how to change it | With their code |

Code layout is not here — that's `README.md` § Layout.

Each file has exactly one job. If two files would say the same thing, one of them is wrong.
**One deliberate exception:** `README.md` § Layout also lists these files, because it's the
GitHub landing page and a human needs the list there. Change one, change the other — it's the
only coupling in the repo, and it's cheap.

**When rules collide**, precedence is: the user's message this turn, then `STATE.md` (what's
actually true now), then this file, then your own judgement. If two sections of *this file*
disagree, say so in **Needs you** rather than picking one silently — that's a bug in the
contract, and it gets fixed once.

---

## 1. What this project is

- Notebook-driven development: a Colab **command center** notebook is both the interface and
  the workspace. Features are built there and extracted to `src/` once settled (§6).
- **The repo exists so the user can understand and build the MVP.** Every file answers
  "what is this, why, what do I change?" A correct repo the user can't reason about has failed.
- We may follow **one or more references** (repos, sites, papers, products). We replicate them
  *our way*; ending up somewhere different is an acceptable outcome, not a failure.
- **The repo is the memory.** A fresh agent reading `STATE.md` + `README.md` + `PLAYBOOK.md`
  (§2, in that order) must be able to continue correctly. Knowledge that exists only in chat is lost.

---

## 2. Session start, then the loop

### First session on a new project

**If `START_HERE.md` exists, the repo is a fresh copy of the template and has never been made
specific to anything.** Read it and follow it before doing anything else — including before
answering whatever the user opened with. It is a step-by-step interview that turns the template
into their project: purpose, references, paths, identity. It deletes itself at the end, so this
branch is taken exactly once in a repo's life.

If it doesn't exist, onboarding already happened. Use the loop below.

### Every session

**Session start:** read `STATE.md`, then `README.md`, then `PLAYBOOK.md`, then skim only the
code the next item touches. Open with ≤5 lines: where we are → proposed next step → why it's
next. `git log` has the detailed chronology; `STATE.md` deliberately doesn't.

If you had to **ask the user something the repo should already have answered**, or re-derive
something you could have read, write the answer down in the same PR. Where it goes: an
environment quirk, a manual step or a dead end → `PLAYBOOK.md`; where the project stands →
`STATE.md`; what a module does or how to change it safely → its docstring. The test is simply
whether the next session would have to ask the same question again.

1. **Propose** the next feature, ordered from repo state + reference. One line on why now.
2. **Frame** it: purpose, 1–2 alternatives, your pick, the tradeoff. Skip for routine plumbing.
3. **Wait for `go`** only where §3 says ask. `go` = the user's answer to your proposal.
4. **Implement.** Docstrings always land with the code, wherever it lives. Anything already in
   `src/` gets its tests in the same change, not later. Formal test *files* for notebook code
   wait for the extraction PR (§6) — but run the cheap checks yourself first: does the notebook
   still parse, does the module import, does the function return what you claim on one small
   input. The user's run should fail on a question of judgement, never on a typo you could have
   caught in seconds.
5. **Verify** — the fastest possible proof it works (§8).
6. **Land** — merge once CI is green.
7. **Update `STATE.md` when the project actually moved** — a step landed, was reverted, got
   parked, or the queue changed order. *Not* for a bugfix, a CI fix, a doc correction or a
   second attempt inside a step that's already listed; `git log` carries those, and `STATE.md`
   stays readable by leaving them out. If you're unsure an entry earns its place, it doesn't.
   `README.md` only when the layout or pipeline actually changed — during exploration that
   normally means at extraction (§6), not every step.

One feature at a time. Finish it, or park it explicitly in `STATE.md`.

---

## 3. Autonomy — act vs ask

**Act. Do not ask.**
- Code edits, refactors, renames, tests, docstrings, comments
- Commits, branches, PRs, CI fixes, dependency pinning
- Merging a PR once its CI is green
- Routine mechanics: formatting, lint config, `.gitignore`, small file moves
- Updating `STATE.md`, `README.md`, `PLAYBOOK.md`

**Ask first, then act on the answer.** One question, with your recommendation.
- Which feature is next, when more than one order is defensible
- A library, service or data format that would be costly to swap later
- A change to the public shape of an existing feature
- Deleting work, force-pushing, rewriting history
- Anything that costs money or leaves the repo
- **Any real ambiguity.** If the purpose, scope or expected output isn't clear, ask before
  implementing.

**`go` means:** implement everything you proposed and merge when CI is green. Full
authorization. Don't re-confirm, don't restate the plan back.

---

## 4. Engineering rules

- **Best common practice by default.** Don't reinvent the wheel unless told to.
- **Prefer the slightly harder path** when it's more reliable or cheaper to live with later.
- **Reversible.** A feature should be removable without archaeology: one PR, isolated module,
  documented seam. Experiments that die should die cleanly.
- **No entanglement.** If changing one line forces edits across many files, the design is
  wrong — fix the seam rather than propagate the edit. Flag it as it forms.
- **Surgical edits.** Touch only what the step needs.
- **Keep the repo small.** Code, config, docs. No scaffolding "for later", no decorative files,
  no boilerplate nobody reads. If a file has no current job, it doesn't exist.
- **Feature docs live in the code** — module or function docstring: what it does,
  inputs/outputs, what to change to modify it safely. No parallel doc file to drift.
  When they're written: §6.
- **Docs are updated when they become wrong, not on a schedule.** One job per file keeps those
  updates to a line or two. If keeping a doc current feels like busywork, the doc is wrong.

---

## 5. The command center notebook

The notebook is both the interface and the workspace: setup, the config cell, features being
built (§6), calls into `src/` for what's settled, and visual output.

- **Every knob lives in the notebook's config cell**, including ones that have settled into
  defaults. The command center is where the user sees and changes things; modules take values
  as arguments rather than reading a config module behind the user's back.
- **The config cell is self-contained.** Reading it alone should tell the user what they can
  change, what the alternatives are, and *why the current value won*. Record the variants
  considered — that's the part that gets forgotten. Group by the decision the user is making.
  Style is yours to pick; be consistent within the notebook rather than following a template.
- **Tests never live in notebook cells.** They live in `tests/` and run in CI or the terminal,
  so test output never piles up in the notebook. Run output is stripped on push by CI, so it
  never reaches git either (`PLAYBOOK.md`).
- Cells run top-to-bottom on a fresh runtime. No hidden state, no out-of-order dependencies.
- The user edits the notebook in Colab and commits with **Save in GitHub** (`PLAYBOOK.md`),
  usually after your step has landed — default values, personal touches. They save before
  saying `go`, so the notebook in the repo is the current one. Work from it as-is.

---

## 6. Feature lifecycle — build in the notebook, extract later

**The notebook is where things get built.** Everything starts there, including multi-step and
inherently entangled features — those get *more* cells, not fewer, so each part produces output
the user can check against what they expected. Never move work into `src/` to make it tidier
while it's still being figured out; that hides it from the person who has to verify it.

**Extract once it's solid** — it works, the user has verified it, and the shape has stopped
changing. Extraction is its own PR with **no behaviour change**: the code moves into
`src/<pkg>/`, the notebook keeps the knobs, the call, and the visual output. Extract when the
feature is settled, when another part needs it, or when the cells have outgrown the workspace —
not on a schedule.

An extracted feature has:
1. A module under `src/<pkg>/` with a docstring: purpose, inputs/outputs, safe knobs.
2. Its knobs still in the notebook config cell, with alternatives and rationale.
3. One call site in the pipeline, and its line in `README.md`'s pipeline section.
4. Tests in `tests/`.

`src/<pkg>/` is the archive of what's settled. The notebook is the workspace.

**While exploring, don't document a moving target.** During expansion the notebook is allowed to
be messy. `README.md` and test files catch up at extraction, in one pass, when the shape has
stopped moving — rewriting a test against a signature that changes next iteration is the
busywork §4 forbids.

Two things never wait:
- **Docstrings.** Every function carries one from the moment it's written, in the notebook cell,
  so the user can read the cell and check it does what it claims. They travel with the code on
  extraction. They're a paragraph, not a chore.
- **`STATE.md`.** Current as of the last step that landed, exploration or not. While `README.md`
  lags reality between exploration and extraction, `STATE.md` is what keeps the user oriented.
  Steps, not attempts — the cadence is §2.7.

**Removing one:** delete its module, its config-cell block, its call site, its tests, its
pipeline line, and note it in `STATE.md` §6 with a one-line reason. If removal touches anything
else, that's an entanglement bug — fix the seam.

---

## 7. Environment — Colab + Google Drive

The user runs, edits and tests in **Google Colab** with **Google Drive** mounted. Assume that,
not a local machine.

- **Only code, config and docs go in git.** Data, weights, caches, outputs and credentials live
  in Drive and are `.gitignore`d. Path *strings* are fine to commit — it's the files that stay out.
- **One Drive root**, set in the notebook config cell and nowhere else — not in `PLAYBOOK.md`,
  not in a module. One place to change means nothing to keep in sync.
- **Secrets never touch the repo** and are never printed in a cell. Colab Secrets, or a file at
  the agreed Drive path.
- **Manual setup is one-time and explicit.** If the user must place a file by hand, give exact
  path, filename and format once, then record it in `PLAYBOOK.md` so it's never asked again.
- Setup is repeatable from a fresh runtime: mount Drive → install → configure → run.
- **Tests run without Drive, network or a GPU** — CI has none of them. Anything needing real
  data takes a path argument and gets a small fixture or a temp dir in tests. If a feature can't
  be tested without Drive, that's a seam problem: the I/O and the logic aren't separated.

---

## 8. Verification is the bottleneck

The user is an amateur in most fields and verifies slower than you produce. Optimize for
*their* check time, not your output volume.

- **You cannot run the notebook.** No Colab runtime, no Drive, no GPU. Anything that only
  proves itself by executing a cell is verified by the user, always. Never write "verified" or
  "confirmed working" about a cell you didn't execute — say what you expect it to print and let
  them check. Getting this wrong is worse than a bug, because it burns their trust in **Done**.
- **Not everything is theirs to check.** Unit tests, lint and CI are yours — run them, report
  the result as one line under **Done**.
- **Verify** carries at most one item, and only if a human must judge it: behaviour, output
  quality, visuals, a design call. Otherwise write "Verify: nothing".
- When there is one, prefer **visual and immediate** — a cell to run, a plot, a printed table.
- Say exactly what a **pass** and a **fail** look like.
- A long verification slog is a signal the step may be too big — say so and offer to split.
  Judgement call, not a rule; exploratory steps are allowed to be long if flagged up front.

---

## 9. How to report

Compartmentalize. Never mix these four.

```
## Done          what changed. informative only, no action needed.
## Needs you     decisions, blockers, ambiguities. numbered, each with your recommendation.
## Verify        the one check to run, and what a pass looks like.
## Next          proposed next step, one line of why.
```

Concise. No preamble, no restating the request, no repeating yourself. If a section is empty,
say so in a word and move on.

---

## 10. `STATE.md` and `PLAYBOOK.md`

`STATE.md` always contains, in this order:
1. **Goal** — one paragraph: what MVP means here, plus references (zero, one, or several).
2. **Done** — every merged step, oldest first, numbered, one line each. Complete enough to scan
   for anything missed, brief enough to stay readable. Detail is in `git log`.
3. **In progress** — at most one. Branch + where it stopped.
4. **Next** — ordered queue to MVP, one line each.
5. **Optional / later** — would step the project up, not blocking MVP.
6. **Parked / dropped** — with a one-line reason, so it isn't re-proposed.

The queue is re-ordered freely as the user redirects; the **Goal** is what stays fixed.
Seeding a fresh `STATE.md` happens once, during onboarding (§2).

`PLAYBOOK.md` holds anything you'd otherwise re-derive: Colab quirks, manual setup steps, run
commands, naming conventions, known-bad approaches, and any correction made more than once.
Not paths — those live in the notebook config cell.
If the user corrects you twice on the same thing, write it there in the same turn.
