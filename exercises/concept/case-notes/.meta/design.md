# Design

## Goal

Introduce `LIST{T}` — a collection that grows — and the distinction between
a container that changes in place and one that answers a new version.

## Learning objectives

- Make a `LIST{T}` and append to it.
- Read and write positions, and remove one.
- Recognise that `append` and `remove_index` change the list and answer
  nothing.
- Say when an `ARRAY` is right and when a `LIST` is.

## Out of scope

- `insert_before`, `copy` and the rest, in the concept page only.
- The cost of appending and of removing from the front, which is explained
  rather than measured.
- Writing a growable list. The point here is to read the library's, now that
  `lost-property` has shown what the braces mean.

## Why this comes after generic-classes

`LIST{T}` could have been taught right after `arrays`, and pedagogically it
belongs there. It is here because `{T}` would have been unexplained
machinery at that point, and the syllabus rule is that nothing appears
before it is taught. The cost is that students write ordinary programs for
sixteen exercises with only fixed arrays; the alternative was hand-waving
the braces.

## Concepts

- `lists`

## Prerequisites

- `arrays`
- `generic-classes`

## Analyzer

None yet. Worth catching: `notes := CASE_NOTES::add_clue(...)`, carried over
from the `FMAP` habit, which does not compile — and the reverse, a student
who has learnt from this that everything changes in place.
