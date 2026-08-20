# Design

## Goal

Introduce `ARRAY{T}`, the literal, indexing from nought, and `.size` — and
join them to the loop from the previous exercise.

## Learning objectives

- Read and write the type `ARRAY{T}`.
- Write an array literal.
- Get a value out by position, counting from nought.
- Reach the last value with `.size - 1`.
- Walk an array with a counting loop.

## Out of scope

- `elt!` and the other iterators, which are what task 5 really wants. Doing
  it by hand first is the point: `bird-survey` then shows the same total in
  two lines.
- Changing an array's contents. Every task here reads.
- `#ARRAY{T}(n)`, which the concept page mentions but no task needs, since
  every array either arrives as an argument or is written as a literal.

## Concepts

- `arrays`

## Prerequisites

- `loops`

## Analyzer

None yet. Task 3 is shaped to catch `row[2]`, which passes on a row of three
and fails on the others; the tests already do that.
