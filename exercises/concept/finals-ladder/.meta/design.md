# Design

## Goal

Use a bound routine for something real: supplying an order to the library's
sort. This is the exercise `understudy` exists to make possible.

## Learning objectives

- Sort with the natural order using `sort`.
- Supply an order with `insertion_sort_by` and a bound routine.
- Write a comparison that answers "does the first come first".
- Order a multi-part rule from most to least important.
- Sort a copy when the original must survive.
- Know that the sorts are not stable, and settle ties in the comparison
  rather than relying on the input order.

## Out of scope

- `binary_search`, `is_sorted_by` and `ARR_SORT_ALG::sort_by`, in the
  concept page only.
- Sorting a `LIST`. `insertion_sort_by` is on `ARRAY`, and converting back
  and forth would be about conversion rather than sorting.
- Writing a sort. The library has several; the skill worth having is
  choosing one and telling it what order to use.

## Concepts

- `sorting`

## Prerequisites

- `arrays`
- `bound-routines`

## Analyzer

None yet. Two worth catching: `>=` in a comparison, which the tests here do
not reliably catch, and task 2 sorting the array it was handed instead of a
copy — which the tests do catch, since task 4 sorts the same array again.

A third, found while writing this: an earlier draft of the concept page said
`insertion_sort_by` was stable. It is not, and the exemplar's tests caught
it. Task 5 now requires a total order, which is what a comparison should be
anyway.
