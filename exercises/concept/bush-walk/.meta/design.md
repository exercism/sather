# Design

## Goal

Write an iterator: `yield`, `quit`, `once`, and the fact that the thing
suspends and resumes.

## Learning objectives

- Write an iterator, ending its name in `!`.
- Hand values over with `yield` and understand that it suspends.
- End one with `quit`, and by running out.
- Yield conditionally, so that a turn may produce nothing.
- Drive one iterator with others.

## Out of scope

- Iterators on an object rather than a class. Every one here is called on
  the class, so `self` never comes up.
- Iterators with no return type, in the concept page only.
- Nested-structure walking, which the concept page shows and which needs
  `ARRAY{ARRAY{T}}` — a type the syllabus has never used.

## Concepts

- `custom-iterators`

## Prerequisites

- `code-inclusion`

## Analyzer

None yet. Worth catching: task 2 yielding before the `quit`, which the tests
do catch, and an iterator written with `return` instead of `yield`, which
does not compile.
