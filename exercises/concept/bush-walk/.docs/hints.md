# Hints

## General

- Every name here ends in `!`, and every one hands values over with `yield`
  rather than `return`.
- Mark the arguments `once`. Nothing here wants an argument re-evaluated
  every turn.
- Test one by writing a loop around it. An iterator cannot be called on its
  own, so there is nothing to print without a `loop`.

## 1. The markers

- A `loop` inside the iterator, driven by `1.upto!(count)`, yielding
  `spacing` times the number.
- Nothing special is needed for a count of nought: `1.upto!(0)` gives
  nothing, so the inner loop ends at once and the iterator is over.

## 2. Until the track ends

- Walk the array with `elt!`, and `quit` when the value is `"end"`.
- The order matters: `quit` before the `yield`, or `"end"` gets handed over
  before you stop.
- Nothing is needed for an array with no `"end"` in it. The `elt!` runs out
  and the iterator is over.

## 3. Only the birds

- Walk the array, and `yield` only inside an `if`. A turn that yields
  nothing simply goes round again — an iterator is not obliged to yield
  every time.
- A name starts with a capital when its first character `.is_upper`.
- Guard against an empty string before reaching for its first character.

## 4. Numbered

- Two iterators inside your own iterator: `1.up!` for the number and `elt!`
  for the sighting. This is the pairing from `duet-practice`, now inside
  something you wrote.
- Build the string with `+`. The number comes first, so start with
  `number.str`, since a string may have a number added to it but not the
  other way round.
