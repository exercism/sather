# Design

## Goal

Introduce `bind`, the `ROUT` types, and `call` — passing behaviour rather
than data, which is the last of the features that make Sather what it is.

## Learning objectives

- Write a `ROUT` type, with argument types and a return type.
- Make a bound routine with `bind` and `_`.
- Call one with `call`.
- Take a bound routine as an argument, and return one.
- Fix some arguments at bind time and leave others as holes.

## Out of scope

- `ITER{...}`, the bound-iterator counterpart, in the concept page only.
- The parser's refusal to accept `return bind(...)`, which is recorded in
  the concept page and the hints because every student will hit it and the
  error message does not explain itself.
- Dispatched bound routines, which this compiler does not implement. The
  concept page says so, because a student who tries it deserves to know it is
  the compiler and not their code.
- The library routines that take bound routines — `sort_by`, `count_if` —
  which are shown in the concept page. Using them would make the exercise
  about the library rather than about binding.

## Why this is last

It is the only feature that needs every other one to be comfortable already:
the tasks pass routines to routines, return them from routines, and build
them out of routines that take arguments. Placed earlier it would compete
with whatever else was new.

## Concepts

- `bound-routines`

## Prerequisites

- `generic-classes`

## Analyzer

None yet. The one to catch is `rehearse` or `run_scene` calling `shout`
directly instead of the bound routine it was handed — which fails the tests
only because they pass `whisper` as well.
