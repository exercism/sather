# Hints

## 1. Who is above whom?

- Two parts, most important first. Settle the points with an `if` that
  returns, and let the goal difference have the last line.
- Both comparisons are `>`, not `<`: more points and better difference come
  *first*.
- Do not use `>=`. A comparison that says a team comes before itself breaks
  the sort.

## 2. The ladder

- `insertion_sort_by` takes a bound routine:
  `bind(higher(_, _))`, with two holes because `higher` takes two teams.
- It sorts in place and answers nothing, so sort a `.copy` and return that.
  Sorting the array handed in would change the caller's.

## 3. Read the ladder out

- A loop and an `FSTR`, with the `", "` before every name but the first.

## 4. The premiers

- Call `ladder` and take `[0]`, rather than working the top out again.
- Check for an empty array first, or `[0]` reads off the end of it.

## 5. A different order entirely

- Write a second comparison routine, on `STR` rather than `TEAM`. It has two
  parts, like `higher`: length first, then alphabetical for equal lengths.
- `<` compares two strings alphabetically, so the tie-break is one line.
- Then the same `.copy` and `insertion_sort_by` as task 2, with the new
  routine bound instead.
