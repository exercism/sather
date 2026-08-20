# Design

## Goal

Teach that a loop ends when the first of its iterators runs out, and that an
endless iterator is useful because of it.

## Learning objectives

- Drive one loop with two iterators.
- Predict how many turns a loop with two iterators takes.
- Pair `up!` with a finite iterator to number items.
- Ask each iterator once per turn.

## Out of scope

- Reaching the elements the shorter array does not cover, which needs
  positions and a guard and belongs to no concept here.
- Writing an iterator, which is `bush-walk`.
- Building a string from the loop, which needs `FSTR` and is the next
  exercise; every answer here is a number.

## Concepts

- `iterator-combination`

## Prerequisites

- `iterators`

## Analyzer

None yet. The mistake to catch is calling the same iterator twice in one
body, which the tests catch only by accident.
