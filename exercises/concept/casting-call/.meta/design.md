# Design

## Goal

Introduce `if` / `elsif` / `else`, and with it the idea that the order of
the tests decides the answer.

## Learning objectives

- Write an `if` with an `else`.
- Extend it with `elsif`, and order the tests from most to least demanding.
- Compare strings with `=` inside a condition.
- Combine a conditional with `and`.

## Out of scope

- `case`, which is what task 3 would really want. It waits for `tram-fares`,
  where the mandatory `else` can be given the attention it needs.
- Loops and everything after them. Each task is still a plain function of
  its arguments.
- Conditionals without an `else`: every routine here returns a value, so
  every branch has to.

## Concepts

- `conditionals`

## Prerequisites

- `booleans`

## Analyzer

None yet. Two things worth catching: a chain written in the wrong order,
which the tests do catch, and `if c then return true else return false end`
appearing now that `if` is available, which they do not.
