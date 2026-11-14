# Design

## Goal

Introduce recursion: a routine that calls itself, a base case, and a
recursive case that gets smaller each time. Several practice exercises
(dominoes, zebra-puzzle, alphametics, killer-sudoku-helper, satellite,
binary-search-tree) are solved by a recursive search, and this gives them a
prerequisite to name.

## Learning objectives

- Write a base case, and check it before recursing.
- Write a recursive case that makes the problem smaller.
- Make more than one recursive call and combine the answers.
- Recurse along an array by passing the position the rest starts at.
- Combine choices with `or`, which stops early.

## Out of scope

- Backtracking with a loop over candidates and mark/recurse/unmark, which is
  what dominoes does. about.md describes it. Task 3 gives the "try one
  choice, then the other" idea without the bookkeeping.
- `shared` state kept across calls, which alphametics and zebra-puzzle use.
- Memoisation and tail calls. about.md mentions why deep recursion can run
  out of stack.

## Concepts

- `recursion`

## Prerequisites

- `arrays`

## Analyzer

None yet. Worth catching: a loop in `acrobats` or `ladder_ways`, which
solves the task without practising the concept.
