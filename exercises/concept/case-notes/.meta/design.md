# Design

## Goal

Introduce `FLIST{T}` — a collection that grows, and that answers the list
to use from now on, which must be assigned back — and `as_array`, the way to
hand the finished list on as an `ARRAY`.

## Learning objectives

- Make an `FLIST{T}` and push onto it, assigning the answer back.
- Know that an empty `FLIST` is void, and which routines cope with that.
- Read positions, and remove one with `delete_ordered`, keeping the order.
- Guard a position with `pre`, and describe a change with `initial` in `post`.
- Turn a finished list into an `ARRAY` with `as_array`.
- Say when an `ARRAY` is right and when an `FLIST` is.

## Out of scope

- `insert_before`, `copy`, `delete` and the rest, in the concept page only.
- `LIST{T}`, the in-place version, which is mentioned on the concept page
  only. Teaching both would mix two habits that look alike.
- `ARRAY{T}::create_from`, which works on an `FLIST` but copies everything
  twice. `as_array` is the one to use.
- The cost of appending and of removing from the front, which is explained
  rather than measured.
- Writing a growable list. The point here is to read the library's, now that
  `lost-property` has shown what the braces mean.

## Why this comes after generic-classes

`FLIST{T}` could have been taught right after `arrays`, and pedagogically it
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
- `contracts`

## Analyzer

None yet. Worth catching: `notes.push(clue);` or `notes.delete_ordered(i);`
with the answer thrown away. The `push` one does not compile, but the
`delete_ordered` one does: the library also has a form that answers nothing.
Also worth catching: `delete` where `delete_ordered` was meant.
