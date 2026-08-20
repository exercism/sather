# Design

## Goal

Introduce `STR`, joining with `+`, and the three routines a beginner needs
most: `.size`, `.head` and `.tail`.

## Learning objectives

- Write a string literal and a routine that returns one.
- Join strings with `+`, and notice that `+` adds no spaces.
- Use `.size` to get a length, and recognise that the length is an `INT`.
- Take the front or the back of a string with `.head` and `.tail`.

## Out of scope

- Indexing a single character out of a string. `CHAR` has no meaning to the
  student yet; it arrives in `cipher-wheel`.
- Building a string in a loop, which is what `rehearsal-script` is for. Every
  task here joins a fixed number of pieces.
- `.upper`, `.lower` and comparison, which are mentioned in the concept page
  but not needed by any task.

## Concepts

- `strings`

## Prerequisites

- `basics`

## Analyzer

None yet. The mistake worth catching later is task 5 spelling out
`title.head(6)` as six separate calls, or using `.tail` where `.head` is
meant, which the tests already catch.
