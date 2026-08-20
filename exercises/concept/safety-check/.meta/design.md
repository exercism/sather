# Design

## Goal

Introduce `BOOL`, the comparison operators, and `and`, `or` and `~`, before
any conditional exists to hide them inside.

## Learning objectives

- Declare a routine returning `BOOL`.
- Produce a `BOOL` by comparing two numbers.
- Combine booleans with `and`, `or` and `~`.
- Return a comparison directly rather than choosing between `true` and
  `false`.

## Out of scope

- `if`. Deliberately: a student who meets conditionals first will write
  `if x then return true else return false end` for the rest of their life.
  Conditionals arrive next, in `casting-call`, once booleans stand on their
  own.
- Short-circuit evaluation, which is in the concept page but which no task
  can show without something observable to skip.

## Concepts

- `booleans`

## Prerequisites

- `basics`

## Analyzer

None yet. The obvious target is `if c then return true else return false
end`, which task 4 is shaped to provoke and which the tests cannot tell
apart from the good answer.
