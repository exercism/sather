# Design

## Goal

Introduce library iterators, and the rule that an iterator only exists
inside a loop. Everything here was possible last exercise with a counter;
the point is how much shorter it becomes.

## Learning objectives

- Call `elt!` to walk an array's values.
- Call `upto!` to count without a variable.
- Recognise that a loop ends when its iterator runs out.
- Keep the result in a variable declared outside the loop.
- Know that writing the same iterator call twice in one body starts two
  independent walks.

## Out of scope

- More than one iterator in a loop, which is the whole of `duet-practice`
  and is deliberately left alone here.
- Writing an iterator, which needs `yield` and waits for `bush-walk`.
- `ind!`, `downto!` and `times!`, which are in the concept page but which no
  task needs; task 5 uses `upto!` over positions because the answer is a
  position.

## Concepts

- `iterators`

## Prerequisites

- `arrays`

## Analyzer

None yet. Two things worth catching: `counts.elt!` written twice in one
loop body, and task 5 solved without `break!` so that the *last* busy day is
returned — the tests catch the second.
