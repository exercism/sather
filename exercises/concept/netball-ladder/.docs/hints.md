# Hints

## General

- Each routine takes whole numbers in and gives a whole number back, so both
  the arguments and the answer are `INT`.
- Two arguments of the same type can share a declaration:
  `ladder_points(wins, draws : INT) : INT`.

## 1. Ladder points

- Multiply each result by what it is worth, then add.

## 2. Goal difference

- Subtraction. Sather is happy with a negative answer.

## 3. Whole quarters played

- `/` between two `INT`s already throws the remainder away, so no rounding
  is needed.

## 4. Minutes into the quarter

- `%` gives exactly what `/` discarded.
