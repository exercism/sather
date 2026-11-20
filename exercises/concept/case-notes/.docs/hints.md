# Hints

## General

- The type is `FLIST{STR}` throughout — a list of strings. Write it out in
  full wherever a notebook goes in or comes out.
- Every routine that changes the notebook answers the notebook to use from
  now on. Inside such a routine, return what `push` or `delete_ordered`
  answered.

## 1. Open a case

- `#FLIST{STR}` makes an empty one. The routine takes no arguments and
  returns `FLIST{STR}`.
- An empty list is void. That is fine: `size`, `push`, `elt!` and
  `as_array` all cope with it.

## 2. Write a clue down

- `push` is the routine, and its answer is the longer notebook. Return it.
- The postcondition goes between the return type and the `is`. `result` is
  the notebook being answered; `initial(notes.size)` is the size of the one
  that came in.

## 3. How many clues?

- `.size`.

## 4. Rule one out

- `delete_ordered` takes the position and keeps the rest in order. Plain
  `delete` moves the last clue into the gap, which muddles the order.
- A routine can have both: `pre` first, then `post`, then `is`.
- Positions count from 0, so the last clue is at one less than the size.

## 5. Read the case back

- A loop with `elt!` and an `FSTR`, as in `rehearsal-script`.
- The `"; "` goes before every clue except the first, which is what makes an
  empty notebook come out as the empty string with no special handling.

## 6. Hand the clues over

- `as_array` makes an `ARRAY` holding the list's values, in order.
