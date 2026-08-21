# Hints

## 1. How many line-ups?

- `#INTI(n).factorial` does the whole job.
- Check what it gives for nought before writing anything special: factorial
  of nought is one, which is the answer the task asks for.

## 2. Write it out

- `.str` on the answer to task 1. Call `line_ups` rather than working the
  factorial out a second time.

## 3. One act's share

- `#RAT(1, acts)` — the numerator first, then the denominator.

## 4. Two acts together

- `+` works on two `RAT`s and gives an exact answer. There is nothing to
  reduce afterwards: a `RAT` is always in lowest terms already.

## 5. Does it fill the show?

- Compare with `#RAT(1)`, or with `#RAT(1, 1)`. Both are the number one.
- `=` on two `RAT`s compares the fractions, so this is a single comparison —
  no `if` and no converting to `FLTD`. Converting would reintroduce exactly
  the rounding this type exists to avoid.
