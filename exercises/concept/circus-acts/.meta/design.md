# Design

## Goal

Introduce abstract classes, conformance with `<`, and dispatch — and the
payoff, which is code that does not have to be changed when a new kind
arrives.

## Learning objectives

- Declare an abstract class with `$` and signatures only.
- Make a class conform with `<` and supply every routine.
- Declare a variable or array of an abstract type.
- Let dispatch choose the implementation instead of asking what type it is.

## Out of scope

- `typecase`, which is in the concept page and which the tasks are shaped to
  make unnecessary. A student who reaches for it here has missed the point.
- Conforming to several abstract classes, and abstract classes extending one
  another.
- `include`. Keeping conformance and code reuse apart is the whole reason
  Sather has both, and running them together here would blur it. It is
  `troupe-routines`, two exercises later.

## Concepts

- `abstract-classes`

## Prerequisites

- `classes-with-state`

## Analyzer

None yet. The one to catch is a `typecase` in `CIRCUS_ACTS`, which passes
every test and is exactly what the exercise exists to avoid.
