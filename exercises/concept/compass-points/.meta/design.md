# Design

## Goal

Introduce `immutable class`, and with it the difference between a value and
a reference.

## Learning objectives

- Declare an immutable class.
- Write a `create` without `new`, starting from `b : SAME`.
- Use the attribute routine that answers a changed copy.
- Write `is_eq` so that `=` works, and `str` so that printing does.
- Say when a thing should be a value and when it should be an object.

## Out of scope

- The storage and copying consequences, which the concept page describes and
  which nothing here can show.
- `$STR` conformance, which writing `str` gives for free and which nothing
  needs to be said about at this point.

## Concepts

- `immutable-classes`

## Prerequisites

- `classes-with-state`

## Analyzer

None yet. Worth catching: a `create` that tries to use `new`, which does not
compile, and `turned` written as though it changed the object, which does
not either. Both fail loudly, which is the argument for immutability in
miniature.
