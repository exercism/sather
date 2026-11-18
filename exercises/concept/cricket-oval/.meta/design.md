# Design

## Goal

Introduce the maths routines on `FLTD` — `FLTD::pi`, `.sqrt`, `.sin`,
`.atan2`, `.exp` and `.log` — and the one trap they share: angles are in
radians.

## Learning objectives

- Call a maths routine on the number it works on, `x.sqrt` rather than
  `sqrt(x)`.
- Use `FLTD::pi`, a routine called on the class rather than on a number.
- Convert degrees to radians before `.sin`, and radians to degrees after
  `.atan2`.
- Know `.atan2`'s argument order: called on the `y` distance, given `x`.
- Use `.exp` for steady decay, and `.log` to undo it.

## Out of scope

- `.hypot`, which the runner's compiler does not build (the generated C
  calls `hypot` with too few arguments). Task 2 uses `.sqrt` instead.
- `.pow`, `.log10` and the rest of the table in the concept's about.md: they
  are called the same way and need no task of their own.
- `NaN` and infinity. No test passes an argument outside a routine's domain.

## Concepts

- `math-functions`

## Prerequisites

- `floating-point`

## Analyzer

None yet. Tasks 3 and 4 are shaped around forgetting the radians
conversion, which no test value forgives. Task 4 has no 90 degree test:
sin(π) comes out as about 8e-15 rather than 0, which is the floating-point
lesson, not this one.

Every expected value prints the same at six significant digits whichever
order a student multiplies and divides in.
