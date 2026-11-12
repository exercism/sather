# Hints

## 1. How many line-ups?

- `factorial` on an `INTI` does the whole job. Make the `INTI` from the
  `INT` first.
- Check what it gives for nought before writing anything special: factorial
  of nought is one, which is the answer the task asks for.

## 2. Write it out

- `.str` on the answer to task 1. Call `line_ups` rather than working the
  factorial out a second time.

## 3. One act's share

- `#RAT(a, b)` makes the fraction `a/b`: the numerator first, then the
  denominator.

## 4. Two acts together

- `+` works on two `RAT`s and gives an exact answer. There is nothing to
  reduce afterwards: a `RAT` is always in lowest terms already.

## 5. Does it fill the show?

- The whole show is the number one. `#RAT` with a single whole number
  makes that number as a `RAT`.
- `=` on two `RAT`s compares the fractions, so this is a single comparison —
  no `if` and no converting to `FLTD`. Converting would reintroduce exactly
  the rounding this type exists to avoid.
