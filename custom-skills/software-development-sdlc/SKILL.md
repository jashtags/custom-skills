---
name: software-development-sdlc
description: End-to-end methodology for approaching a software development task, from ambiguous request to verified, shipped code. Use this whenever asked to build, fix, or modify software of non-trivial size (roughly: touches more than 2-3 files, introduces new behavior, or the right approach isn't obvious). Read this before starting implementation, not after.
---

# Software Development Lifecycle: Operating Approach

This document describes how to move from a request to working, verified,
delivered software. It is stack-agnostic — the same phases apply whether the
task is a web app, a CLI tool, a mobile app, or a backend service. The
through-line is: **resolve ambiguity before writing code, verify behavior
before claiming done, and keep the human informed without burying them.**

## Core principles (apply throughout, not just in one phase)

1. **Ambiguity is resolved before code, not during code review.** If a
   requirement has more than one reasonable interpretation, ask — either with
   a direct question or, for multi-part decisions, a short multiple-choice
   question set. Guessing and hoping to be corrected later wastes more time
   than asking costs.
2. **Compiling is not verification.** A build that succeeds proves the code
   is syntactically and type-valid. It proves nothing about whether the
   feature works. Treat "it compiles" and "it works" as two separate,
   sequential checkpoints.
3. **Match the target ecosystem's idioms.** Use the conventional tools,
   project layout, and patterns for the platform (e.g. Gradle+Kotlin+Compose
   for Android, not a hand-rolled build system). Fighting the ecosystem's
   grain creates bugs the ecosystem would otherwise prevent for free.
4. **Do the smallest thing that fully satisfies the request.** No speculative
   abstractions, no unused configuration options, no "might need this later"
   code. Every added layer is a place a bug can hide and a thing the next
   reader has to understand for no payoff.
5. **Irreversible or shared-visibility actions get a checkpoint.** Local file
   edits, local commits, local test runs: proceed autonomously. Pushing to a
   remote, deleting data, sending messages, spending money: confirm first,
   every time, even if a similar action was approved earlier in the session.
6. **Narrate state changes, not internal deliberation.** The person reading
   your output wants to know what happened and what's next, not the
   step-by-step reasoning that got you there.

---

## Phase 1 — Scope and clarify

Before any design or code:

- Restate the request in your own terms only if genuinely unclear; otherwise
  skip straight to identifying gaps.
- Enumerate the decisions the request doesn't make for you: data storage,
  scope of "done," what happens on edge cases (empty state, concurrent
  access, permission denial), and anything platform-specific the user didn't
  specify (e.g. "the app" without saying which OS, "the database" without
  saying which engine).
- For each gap, decide: is there an obviously-correct, idiomatic default, or
  do multiple reasonable people disagree about the right choice? Idiomatic
  defaults — proceed and state the assumption. Genuine disagreements —
  ask, ideally as a short set of concrete options rather than an open-ended
  question, so the answer takes one tap instead of a paragraph.
- Re-scope questions as new requirements arrive mid-task. A request that
  extends the original scope (e.g. "also add export") deserves the same
  clarify-then-build treatment as the original ask — don't silently absorb
  new scope without a moment's thought about how it fits the existing design.

## Phase 2 — Plan before building

For anything touching more than a couple of files or requiring an
architectural choice:

- Identify the tech stack and justify each non-obvious choice in one line
  (why this database, why this UI framework, why this background-work
  primitive). If the environment already has a convention (existing repo
  patterns, a lockfile, a framework already in use), follow it instead of
  introducing a second way to do the same thing.
- Lay out the file/module structure before writing files, including where
  each responsibility lives (data layer, business logic, UI, background
  work). Vague plans produce inconsistent code; a plan that names files and
  their responsibilities produces code that composes cleanly.
- Describe the behavior of each feature concretely enough that "done" is
  checkable: what triggers it, what state it reads/writes, what the user
  sees, what happens on the edge cases identified in Phase 1.
- Write down how the result will be verified — not "it should work" but the
  actual steps that will be run (which commands, which UI actions, which
  outputs to check). If verification can't be described concretely yet, the
  plan isn't finished.
- Get sign-off on the plan before writing implementation code when the task
  is large enough that a wrong turn would be expensive to unwind. Skip this
  ceremony for small, obviously-scoped changes — it's a tool for aligning on
  direction, not a mandatory gate for every edit.

## Phase 3 — Break work into tracked units

- Split the plan into discrete, ordered tasks, each independently
  completable and independently verifiable. Order by dependency: shared
  primitives (data models, core utilities) before the things that consume
  them (UI, integrations).
- Mark each task's state as work progresses (not-started → in-progress →
  done) rather than holding progress only in memory. This matters most on
  long tasks, where losing track of what's finished leads to redone or
  skipped work.
- When new work is discovered mid-implementation (a missing piece, a new
  requirement from the user), add it as a new tracked task rather than
  quietly folding it into an unrelated one — it keeps the record of what was
  built honest.

## Phase 4 — Implement in dependency order

- Build foundational layers first (data models, storage, core utilities),
  then the logic that depends on them, then the interface on top. Building
  UI against a data layer that doesn't exist yet invites mismatched
  assumptions.
- Kick off slow, independent side-tasks (large downloads, long-running
  installs, environment setup) in the background and continue writing code
  that doesn't depend on their completion, instead of idly waiting.
- Keep each file focused on one responsibility. If a file is accumulating
  unrelated concerns, that's the signal to split it, not a reason to add a
  fourth concern.
- Write no comments that restate what the code does. Write a comment only
  when there's a non-obvious *why* — a constraint, a workaround, an invariant
  the next reader could easily violate without knowing it's there.
- Avoid defensive code for situations that cannot occur given the
  surrounding guarantees. Validate only at real boundaries: user input,
  external APIs, other systems' data.

## Phase 5 — Compile/build checkpoint

- Build (or run the type-checker/linter, whatever the stack's earliest
  correctness signal is) as soon as a coherent unit of work is written —
  don't accumulate ten files of unverified code before the first build
  attempt. Small batches make errors easy to locate.
- Fix the root cause of a build failure, not a workaround that silences it
  (don't suppress a type error by casting to `any`/`Object` when the real fix
  is a type mismatch upstream).
- Once the build is clean, move to runtime verification — a clean build is
  the entry ticket to that phase, not the finish line.

## Phase 6 — Runtime verification (this is where most claimed-done work is actually still broken)

- Run the software in an environment as close to real usage as available:
  an actual emulator/simulator/browser/server, not just a mental trace of the
  code. If no such environment is reachable, say so explicitly rather than
  reporting success on the strength of a build pass alone.
- Exercise the golden path first (the main flow the feature exists for), then
  the edge cases identified in Phase 1 (empty states, permission prompts,
  boundary values, concurrent or repeated actions).
- For anything with a visual surface, look at it — a screenshot or direct
  observation — rather than trusting that the described layout renders as
  intended. Layout and rendering bugs are invisible to a compiler and to
  code review by inspection.
- Read logs/console output for the run, not just the immediate return value —
  crashes, exceptions, and warnings often surface there even when the
  top-level action appeared to succeed.
- Treat every runtime bug found this way as expected, useful signal, not a
  setback: it is the process working as intended. Fix it, then re-verify
  the same path, not just the line that changed.

## Phase 7 — Bug-fix loop

- Reproduce before fixing. Understand *why* the observed behavior happened
  (stale cached state, an unbounded layout constraint, an off-by-one) before
  editing — a fix aimed at the symptom without understanding the cause tends
  to reappear elsewhere.
- After each fix, rebuild and re-run the same verification step that caught
  the bug, plus a quick check that the fix didn't disturb adjacent behavior.
- Keep fixes minimal and scoped to the actual defect. A bug fix is not an
  invitation to refactor unrelated code nearby.

## Phase 8 — Documentation

- Write down how to build/run/test the project, aimed at someone with no
  prior context: prerequisites, the exact commands, and what "working"
  looks like.
- Include a concrete manual test script (numbered steps, expected result at
  each step) for anything that can't be fully covered by automated tests —
  this is what turns "I built it" into "here's how you confirm it works."
- Document *why* non-obvious architectural choices were made, briefly, next
  to where they live — not in a separate essay nobody will read later.
- Don't write documentation that merely restates the code (a function-by-
  function narration). Write what a future reader can't get by reading the
  code themselves: setup steps, rationale, and how to verify correctness.

## Phase 9 — Version control and delivery

- Keep machine-specific and secret files out of version control from the
  first commit (local paths, credentials, generated build output) —
  retrofitting a `.gitignore` after secrets are already committed is a much
  bigger problem than writing it up front.
- Write commit messages that explain *why* the change exists, not a
  restatement of the diff — the diff already shows what changed.
- Review what's actually staged before committing, especially after a broad
  "add everything" — it's the last cheap checkpoint before something
  unwanted becomes permanent history.
- Local commits are low-risk and don't need permission. Pushing to a shared
  remote, force-pushing, or any action visible to other people or systems
  gets a confirmation step first, regardless of what was approved earlier in
  the session.

---

## Communication norms throughout

- State what you're about to do in one sentence before doing it; report
  results directly afterward. Skip narrating the reasoning in between.
- Surface a finding the moment it changes the plan (a failed download, a
  bug found during testing, a scope-changing new requirement) rather than
  batching it into a final summary.
- When something can't be verified (no device/emulator available, no way to
  run the code in this environment), say that plainly instead of implying
  success on weaker evidence.
- End with a short summary of what changed and what, if anything, remains —
  not a replay of every step taken.

## Anti-patterns to avoid

- Treating "the build passed" as equivalent to "the feature works."
- Writing speculative abstractions or config options for requirements that
  don't exist yet.
- Silently expanding scope when new requirements arrive mid-task instead of
  briefly registering how they change the plan.
- Nesting unbounded scrollable/flexible containers inside each other without
  checking that layout constraints actually resolve (a generalizable version
  of "check that the composition of two components is valid, not just that
  each is valid alone").
- Fixing a symptom in the UI/output layer when the actual defect is a stale
  cache, an unbounded query, or a race condition further down — trace to the
  real cause before patching.
- Pushing, force-pushing, or otherwise publishing changes without an explicit
  go-ahead, even inside an otherwise autonomous session.
- Padding documentation or comments with restatements of what the code
  already makes obvious, at the cost of omitting the *why* that's actually
  useful.
