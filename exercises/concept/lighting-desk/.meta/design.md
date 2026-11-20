# Design

## Goal

Treat an `INT` as a row of yes-or-no flags: read one, make one, set, clear
and flip one, and move a group of them with a shift.

## Learning objectives

- Read a bit with `.bit`.
- Make a single-bit mask with `lshift`.
- Set, clear and flip a bit with `bor`, `band` with `bnot`, and `bxor`.
- Pick out a field of bits with `rshift` and a `band` mask.

## Out of scope

- `urshift`, and what shifting does to negative numbers. The introduction
  shows them; no task needs a negative rig.
- `set_bit` and `unset_bit`. They are in the concept's about page, but
  tasks 3 and 4 are there to be built from `bor`, `band` and `bnot`.
- Counting the lights that are on. That is `eliuds-eggs`, a practice
  exercise that has `bits` as a prerequisite.

## Concepts

- `bits`

## Prerequisites

- `numbers`
- `booleans`
- `exact-numbers`, which puts `bits` last in the syllabus. Nothing else
  depends on it, and its practice users mostly wait for `lists` or
  `exact-numbers` anyway.

## Analyzer

None yet. A student can pass task 3 with `+` on rigs where the light is
off; the "already on" test catches that, and task 4's "already off" test
catches `-`.
