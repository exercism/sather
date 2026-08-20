# Hints

## General

- Every loop here is driven by an iterator, so none of them needs a counter
  variable or an `until!`.
- The answer always lives in a variable declared before the loop, because
  anything declared inside disappears when the loop ends.

## 1. The total

- `counts.elt!` gives one count each time round.
- Start the total at `0`, which also gives the right answer for a survey
  with no days.

## 2. The best day

- Keep the best seen so far in a variable, starting at `0`.
- Each time round, compare and replace if this day beats it. `.max` does the
  comparison in one step: `best := best.max(counts.elt!)`.

## 3. The busy days

- Count rather than add: `if counts.elt! > n then found := found + 1; end;`
- Ask the iterator once, inside the `if` condition. Writing `counts.elt!`
  twice in one body walks the array twice over.

## 4. Hides to check

- Nothing is being walked here, so `elt!` is no use. `1.upto!(days)` counts
  for you.
- `1.upto!(0)` gives nothing at all, which is the right answer for nought
  days.

## 5. The first busy day

- The answer is a position, not a value, so walk the positions:
  `i ::= 0.upto!(counts.size - 1)`.
- Start the answer at `-1`. If nothing is found, that is already what should
  be returned.
- Once a day is found, `break!` out — otherwise a later busy day would
  overwrite the first one.
