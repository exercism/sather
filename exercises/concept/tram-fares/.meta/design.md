# Design

## Goal

Introduce `case`, and give the mandatory `else` the attention it needs —
this is the one place where Sather differs from what a student may expect
in a way that fails at run time rather than at compile time.

## Learning objectives

- Write a `case` with `when` arms and an `else`.
- List several values in one `when`.
- Use `case` on `INT`, `CHAR` and `STR`.
- Know that an unmatched `case` without an `else` is a run-time error, not a
  no-op.
- Recognise when a chain of ranges wants `if` instead.

## Out of scope

- `case` on a type, which is what `typecase` is for and which needs
  subtyping.
- `raise` in the `else`, which is what the honest answer would be for an
  unknown zone. Exceptions arrive in `missing-props`; until then the tasks
  are worded so that a default value is a real answer rather than a fudge.

## Concepts

- `case-statements`

## Prerequisites

- `iterator-combination`

## Analyzer

None yet. Two things worth catching: a `case` written where the tests
happen to cover every arm so the missing `else` never fires, and task 4
repeating the day names instead of calling `day_type`.
