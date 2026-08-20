# Design

## Goal

Introduce `FSTR`, and with it the reason it exists: `+` on `STR` inside a
loop does work proportional to the square of the length.

## Learning objectives

- Create an `FSTR`, add to it in a loop, and finish with `.str`.
- Assign the result of `+` back into the builder every time.
- Explain why `STR` and `+` are wrong inside a loop and right outside one.
- Add a `CHAR` and an `INT` to a builder without converting them first.

## Out of scope

- `.clear`, `#FSTR(n)` and the rest of the interface, which the concept page
  lists but no task needs.
- Anything requiring the student to measure the difference. The quadratic
  cost is explained rather than demonstrated: at the sizes these tests use,
  both versions are instant, and a task that only passed for the right
  reason would need timings the harness cannot take.

## Concepts

- `string-builders`

## Prerequisites

- `characters`

## Analyzer

None yet, and this is the exercise that most wants one: every task here
passes its tests just as well when written with `STR` and `+`, so only a
reader — or an analyzer — can tell whether the concept landed.
