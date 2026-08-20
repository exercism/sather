# Design

## Goal

Introduce `FLTD`, the `d` literal, and division that keeps a fraction —
against the integer division taught in `netball-ladder`.

## Learning objectives

- Write an `FLTD` literal, with both the decimal point and the `d`.
- Divide without losing the remainder.
- Convert an `INT` with `.fltd`, and know that it must happen before the
  division.
- Use `.abs` for a distance between two values.

## Out of scope

- Comparing floating-point values, which is why no task asks for one and
  every test compares an `FLTD` against an `FLTD` computed the same way.
  The trap is described in the concept page, where it can be explained
  rather than sprung.
- `%`, which `FLTD` does not have.
- Rounding and formatting for display, which needs the format classes.

## Concepts

- `floating-point`

## Prerequisites

- `loops`

## Analyzer

None yet. Task 5 is shaped around the one mistake worth catching:
`(minutes / players).fltd`, which loses the fraction before converting and
which no test value can be chosen to forgive.
