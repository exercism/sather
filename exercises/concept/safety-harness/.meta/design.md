# Design

## Goal

Introduce `pre` and `post`, and the distinction between a contract and an
exception.

## Learning objectives

- Write a `pre` on a routine's arguments.
- Write a `post`, using `result`.
- Join conditions with `and`.
- Say when a contract is right and an exception is right.
- Know that contracts are checked only under `-chk`, and that a violation
  stops the program rather than raising.

## Out of scope

- `invariant` and `assert`, which are in the concept page. Both need a class
  doing more than this one to be worth writing.
- Contracts under inheritance, which needs subtyping and is described in the
  concept page only.

## A limitation worth recording

The track's test runner compiles without `-chk`, so no test here can check
that a contract *fires*. The tests exercise the routines within their
contracts and check the answers. This is a real gap: a student who writes
`pre load < 0` by mistake passes.

Closing it would mean the runner compiling each exercise twice, or a
per-exercise compiler flag, neither of which exists. Until then the contracts
are reviewed rather than tested, and task 4 is worded to make the intended
`post` unambiguous.

## Concepts

- `contracts`

## Prerequisites

- `classes-with-state`

## Analyzer

None yet, and this exercise needs one more than most: the contracts are the
whole point and nothing checks them. An analyzer that confirmed each routine
carries the clauses the instructions ask for would close most of the gap.
