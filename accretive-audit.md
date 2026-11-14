# Accretiveness audit — Sather concept exercises

## What "Accretive" means

A concept exercise ships a stub in which every routine body is
`raise "unimplemented";`. The exercise is **Accretive** if a student who
correctly implements the first *K* tasks (obeying every instruction for those
tasks) and leaves the remaining tasks as stubs sees **all tests for tasks 1..K
pass**.

We want every concept exercise to be Accretive.

## How an exercise fails to be Accretive

`sacomp` compiles the solution, the test file and the harness as one program
before any test runs, and the first uncaught exception ends the run (the test
runner keeps the results reported so far and says the suite stopped early).
That gives these failure modes.

**Mode A — compile-time.** The test file names a class, routine, attribute or
iterator that the stub does not declare. Until the student writes it, nothing
compiles, so **no** task passes. If the missing definition is created in
**task 1**, the exercise is still Accretive: doing task 1 makes the program
compile (`circus-acts`, whose task 1 is writing the three act classes).

**Mode B — runtime.** A test for task *K* calls a routine the instructions
assign to a later task *M > K*. The program compiles, but that routine still
raises, so task *K*'s test fails even though the student did tasks 1..K
correctly. This typically happens for stateful classes and containers whose
task-*K* behaviour is *observed* through a later task's routine.

**Ordering.** Because a raise ends the run, every test for tasks 1..K must come
before the first test (or set-up statement) that reaches a later task's
routine. Otherwise an early task's tests are never reached.

**Structural.** The test file is not grouped into tasks by `-- Task N` marker
comments, so no prefix of tasks can be checked.

## Methodology

Verified empirically with the test runner image, via `bin/check-accretive`.

- Each `<slug>_test.sa` marks its task groups with `-- Task N` comment lines.
  Every `test("name", ...)` belongs to the nearest marker above it.
- Each `.meta/ownership.json` maps every routine, by `CLASS::name` (or a whole
  `CLASS`), to the task that implements it.
- **Mode A:** run the shipped stub against the tests. It must compile, unless
  ownership says `"requires-task1-to-compile": true`.
- **Mode B and Ordering:** for each prefix *K*, rebuild the exemplar with every
  unit owned by a task *> K* replaced by the stub's version of that unit, run
  it, and check that every test for tasks 1..K is reported as passing.
- It also checks that the markers cover tasks 1..N of the instructions, in
  order, and warns when a routine is not mentioned in its task's section of the
  instructions.

Run it with `bin/check-accretive [-i IMAGE] [slug...]`. It uses
`exercism/sather-test-runner:latest` by default and never pulls it.

## Results

Before this audit the stubs were comments ("Write your routines between here
and the end of the class."), so **all 26 concept exercises were Mode A**. Seven
of them also had Mode B or Ordering problems, which surfaced while grouping
their tests by task. (`finals-ladder` and `case-notes` were also confirmed by
running the checker against their old tests.) All have been fixed, and
**every concept exercise is now accretive (26/26)**. `human-pyramid`,
added afterwards, was written accretive and passes the checker (27/27).

| Original verdict | Count | Exercises |
|---|---|---|
| Mode A only (fixed) | 19 | bird-survey, casting-call, cipher-wheel, circus-acts, compass-points, dance-formation, duet-practice, formation-count, missing-props, netball-ladder, programme-notes, rehearsal-script, safety-check, stage-directions, tram-fares, troupe-routines, tuning-the-strings, understudy, warm-up-laps |
| Mode A + Mode B (fixed) | 6 | case-notes, field-guide, finals-ladder, lost-property, safety-harness, scoreboard |
| Mode A + Ordering (fixed) | 1 | bush-walk |

## Mode A — the stubs declared nothing (fixed)

Every stub now declares every class, attribute, routine and iterator the tests
need. Each routine has its signature from the exemplar, without its `pre`/`post`
(writing contracts is part of several lessons), and the body
`raise "unimplemented";`. Classes that the stub already supplied (`TEAM`,
`WARM_UP`, `$ACT`) are unchanged.

Two exceptions:

- **circus-acts** — task 1 *is* writing `JUGGLING`, `TUMBLING` and `TRAPEZE` as
  subtypes of `$ACT`, so the stub leaves them out and the exercise is
  accretive-via-task-1. `CIRCUS_ACTS` (task 2) is declared.
- **safety-harness** — `invariant` is checked on entry to and exit from every
  public routine, so a raising placeholder would break every task. Its
  placeholder answers `true`, and the instructions say why.

The instructions no longer say "write X below it"; they describe the stub
instead. **finals-ladder** task 5 now names `shorter`, which the tests call
directly but the instructions never mentioned.

## Mode B — an early task's test called a later task's routine (fixed)

All six were fixed with test-only changes. Each forward-referencing assertion
moved into the task that owns the routine, or the early task observes its
result through the library instead.

- **case-notes** — tasks 1–2 observed the notebook through `clue_count`
  (task 3) and `summary` (task 5). They now use `notes.size` and `notes[i]`;
  the `summary` checks moved to task 5 with a notebook of their own.
- **field-guide** — the `add_entry` tests (task 3) counted through
  `entry_count` (task 4) and came after the task 4–5 tests. They now count with
  `FMAP`'s `size`, come before task 4, and build their own guide.
- **finals-ladder** — the `ladder` tests (task 2) read the result through
  `names` (task 3). They now read `ranked[i].name`, and a new task-3 test names
  the ranked ladder.
- **lost-property** — task 1's block also exercised `waiting` (task 3) and
  `describe` (task 5). The tests are regrouped by task.
- **scoreboard** — every block checked `summary`, `leader` and `margin`
  (tasks 3–5) alongside the goals. Tasks 3–5 now each have a board of their own.
- **safety-harness** — the second-harness block mixed tasks 1–4. Its checks
  moved into their own tasks.

## Ordering (fixed)

- **bush-walk** — "each call site keeps its own place" tests `markers!`
  (task 1) but came last. It moved into task 1.

## Track rules (to keep new exercises Accretive)

1. The stub must make the test file compile on its own. Declare every class,
   attribute, routine and iterator the tests use, with
   `raise "unimplemented";` bodies and no contracts, so Mode A is impossible.
   The only exception is a definition that task 1 itself creates
   (`requires-task1-to-compile`). A routine checked implicitly, such as
   `invariant`, must not raise.
2. Group the tests under `-- Task N` markers, in task order. Each task's tests,
   and the set-up statements before them, use only routines from that task and
   earlier ones (no Mode B, no Ordering).
3. Keep `.meta/ownership.json` in step with the instructions.

`bin/check-accretive` enforces all three.
