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
- Write a class `invariant`, allowing for the void `self` it meets on entry
  to `create`.

## Out of scope

- `assert`, which is in the concept page, and needs a routine doing more
  than these do to be worth writing.
- Contracts under inheritance, which needs subtyping and is described in the
  concept page only.

## A limitation worth recording

The track's test runner compiles with `-chk`, so contracts are checked, but
a broken one stops the whole run rather than failing a test. So the tests
stay within the contracts and check the answers, and a contract that is too
strong (`pre load > 0`, say) stops the run at the first load of nought.

No test can check that a contract *fires*: that would mean breaking it, and
stopping the run. So a contract that is too weak passes. Task 5's tests call
`invariant` directly, which requires the routine to exist and to survive a
void `self`, but `return true` passes them. Until an analyzer exists, the
contracts are reviewed rather than tested, and tasks 4 and 5 are worded to
make the intended clause unambiguous.

## Concepts

- `contracts`

## Prerequisites

- `classes-with-state`

## Analyzer

None yet, and this exercise needs one more than most: the contracts are the
whole point and nothing checks them. An analyzer that confirmed each routine
carries the clauses the instructions ask for would close most of the gap.
