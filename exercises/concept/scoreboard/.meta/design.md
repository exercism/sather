# Design

## Goal

Introduce objects: `attr`, `create`, `new`, `SAME`, and routines that change
the object rather than answering.

## Learning objectives

- Declare attributes and know they start empty.
- Write a `create` that uses `new` and returns `SAME`.
- Make an object with `#`.
- Write a routine with no return type that changes the object.
- Use an attribute by name from inside the class.

## Out of scope

- `readonly` and `private`, which the concept page covers but which the stub
  does not use: making the scores settable is one fewer thing in the way,
  and `contracts` is where guarding a change gets its own exercise.
- `self`, which nothing here needs written out.
- Several classes in one file, which starts at `contracts`.

## Concepts

- `classes-with-state`

## Prerequisites

- `case-statements`

## Analyzer

None yet. Worth catching: `create` setting `home_score := 0` explicitly,
which is harmless but suggests the student has not taken in that attributes
start empty.
