# Design

## Goal

Introduce `FMAP` and `FSET`, keyed lookup, and the functional insert that
answers a new container.

## Learning objectives

- Declare and use `FMAP{K,T}` and `FSET{T}`.
- Look up with `get`, and check with `has_ind` first.
- Assign the result of `insert` back, and stop using the old name.
- Know that `get` on a missing key answers an empty value rather than
  failing.
- Use a set to collect values without repeats.

## Out of scope

- `HMAP` and `HSET`, mentioned in the concept page. Meeting the functional
  ones first makes the assign-back rule the default habit.
- Set combination — `union`, `intersect` — which is a second idea and would
  make this two exercises.
- `copy`, and the void-map hole in it. The concept page is honest about
  both, but no task depends on keeping an original intact, because getting
  that right needs a void check that has nothing to do with maps.
- Ordering. Nothing here may depend on the order of a walk, which is why
  task 5 answers a set rather than an array.

## Concepts

- `maps-and-sets`

## Prerequisites

- `case-statements`

## Analyzer

None yet. Two worth catching: `guide.insert(...)` written without using the
answer, and task 2 fetching before asking — which passes every test here,
because a void habitat only fails once something tries to use it.
