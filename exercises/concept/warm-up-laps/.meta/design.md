# Design

## Goal

Introduce `loop`, the two ways of ending one, and the local variable that
every loop needs.

## Learning objectives

- Declare a local variable with `::=` and update it with `:=`.
- Write a `loop` and end it with `until!`.
- End a loop with `break!` from inside a conditional.
- Choose where to put `until!` so that a zero case runs the body no times.

## Out of scope

- Arrays and iterators. Nothing here has a collection to walk, so every
  loop is driven by a counter the student maintains. `bird-survey` later
  shows how much of that the library does already.
- `while!`, which is `until!` with the question the other way round and adds
  nothing new to think about. It is in the concept page, not in a task.
- Building strings in a loop, which needs `FSTR` and waits for
  `rehearsal-script`.

## Concepts

- `loops`

## Prerequisites

- `numbers`
- `strings`
- `conditionals`

## Analyzer

None yet. Worth catching later: solving task 1 with the arithmetic series
formula, which is correct but sidesteps the exercise.
