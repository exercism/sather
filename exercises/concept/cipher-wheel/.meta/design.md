# Design

## Goal

Introduce `CHAR`: how one is written, how it comes out of a string, what can
be asked about it, and the fact that it has a number behind it.

## Learning objectives

- Tell `'a'` from `"a"`.
- Take a character out of a string by position.
- Use `.is_alpha` and `.upper`.
- Move between a character and its number with `.int` and `.char`.
- Wrap a value round with `%`.

## Out of scope

- Walking a whole string a character at a time. That wants `elt!` or a
  loop over positions, and building the result wants `FSTR`; both come
  later, and doing a whole Caesar cipher here would need all of it at once.
- Capital letters in task 5. Handling both cases doubles the arithmetic
  without teaching anything the small letters have not already taught.
- `is_alphanum` and `is_space`, which are in the concept page but which no
  task needs.

## Concepts

- `characters`

## Prerequisites

- `loops`

## Analyzer

None yet. The thing worth flagging is `97` written in place of `'a'.int` in
task 5: correct, and much harder to read.
