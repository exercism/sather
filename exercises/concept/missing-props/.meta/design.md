# Design

## Goal

Introduce `raise` and `protect` / `when`, and the fact that an exception
travels outward on its own.

## Learning objectives

- Raise a string when a routine cannot answer.
- Catch one with `protect` / `when $STR`, and read it with `exception`.
- Let an exception pass through a routine without mentioning it.
- Tell a value that means "none" from a failure to answer.

## Out of scope

- Raising anything but a `STR`. A class carrying structured detail is better
  practice and needs a second class in the file, which is not allowed until
  the next exercise.
- Several `when` arms of different types, which needs the same.
- `protect` around code that raises nothing, and the temptation to wrap
  everything: the concept page argues against it, but no task can show it.

## Concepts

- `exceptions`

## Prerequisites

- `classes-with-state`

## Analyzer

None yet. The one to catch is task 2 repeating the `has_ind` check and the
`"Unknown prop: "` message instead of calling `count_of` — it passes every
test.
