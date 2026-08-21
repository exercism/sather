# Design

## Goal

Introduce the two exact numeric types together, against the two inexact ones
the student already knows — `INT`, which is bounded, and `FLTD`, which is
approximate.

## Learning objectives

- Use `INTI` for a count that outgrows `INT`.
- Make one from an `INT` and read it back as a string.
- Use `RAT` for fractions that must be exact.
- Compare `RAT`s with `=` and rely on the answer.
- Say when the exact types are worth their cost and when they are not.

## Why one concept and not two

`INTI` and `RAT` are the same idea applied twice: give up speed to stop
losing information. `RAT` is built on `INTI`, so they are not even
independent. Teaching them apart would mean making the same argument twice
and inventing a second setting for it.

The cost is that this exercise has two types in it, which is more than the
one-new-idea rule elsewhere allows. The defence is that the idea is one and
the types are two, and that either alone leaves the contrast with `FLTD`
half-made.

## Out of scope

- `gcd`, `pow`, `floor`, `is_int` and the rest, in the concept page only.
- `.int` overflowing silently on a large `INTI`, which is mentioned but which
  no task can show without the test itself being wrong.
- `ceiling`, which raises "not implemented" in this library.

## Concepts

- `exact-numbers`

## Prerequisites

- `numbers`
- `floating-point`

## Analyzer

None yet. Worth catching: task 5 converting to `FLTD` to compare, which
passes these tests and defeats the purpose, and task 1 written as a loop
multiplying `INT`s and converting at the end, which overflows before it gets
there.
