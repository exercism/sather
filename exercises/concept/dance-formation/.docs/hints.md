# Hints

## General

- An array of names has type `ARRAY{STR}`, and an array of numbers
  `ARRAY{INT}`. Both the argument and, in task 4, the answer need to say
  which.

## 1. How many in the row?

- `.size`, with no brackets after it.

## 2. Who leads?

- The first position is `0`.

## 3. Who is at the back?

- The last position is one less than the size, because counting starts at
  nought.
- Work it out from `.size` rather than writing `2`. The tests use rows of
  several different lengths.

## 4. The opening formation

- The answer is an array of strings, so the routine is declared
  `: ARRAY{STR}`.
- Return an array literal: the three names between `|` marks.

## 5. Count the steps

- A running total and a loop, as in the previous exercise.
- Count a position variable from `0` upwards, and end the loop with
  `until!(i >= steps.size)`.
- Starting the total at `0` is what makes the empty row answer nought
  without any special handling.
