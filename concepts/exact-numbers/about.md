# Exact Numbers

| Type | Holds | Limit |
| --- | --- | --- |
| `INT` | whole numbers | exactly 32 bits |
| `FLTD` | fractions | approximate |
| `INTI` | whole numbers | memory |
| `RAT` | fractions | exact |

## INTI

```sather
   #INTI(42)
   #INTI("123456789012345678901234567890")
   a + b, a - b, a * b, a / b
   a < b, a = b
   #INTI(25).factorial
   #INTI(48).gcd(#INTI(18))       -- 6
   #INTI(2).pow(100)
   big.str
   small.int                      -- back to an INT, if it fits
```

`/` on two `INTI`s is integer division, discarding the remainder, exactly as
it is on `INT`.

`.int` on a value too large for an `INT` does not report the problem. Check
first if it matters.

## RAT

```sather
   #RAT(1, 3)
   #RAT(6)                        -- from a whole number
   a + b, a - b, a * b, a / b
   a < b, a = b
   r.is_int                       -- is it a whole number?
   r.is_zero, r.is_pos, r.is_neg
   r.abs, r.negate
   r.floor                        -- an INTI, rounded down
   r.str
```

A `RAT` is always in lowest terms and always carries its sign on top:
`#RAT(1, -2)` is `-1/2`. Two `RAT`s are equal exactly when they are the same
fraction, so `=` does what you want — which is the whole difference from
`FLTD`.

`RAT` is built on `INTI`, so its numerator and denominator have no size
limit either. Adding many fractions with different denominators makes them
grow, since each addition multiplies the denominators out before reducing.

`ceiling` is declared but raises "not implemented". Use `floor` and adjust.

## Choosing

Reach for `INTI` when a count can exceed two thousand million: factorials,
powers, combinations, running totals over a long time.

Reach for `RAT` when fractions must be exact and the denominators are
small-ish: shares, probabilities, musical note values, anything that would
otherwise accumulate rounding error.

Reach for neither by default. `INT` and `FLTD` are far faster, and most
arithmetic does not need more.

For money, neither is the usual answer: count whole cents in an `INT`.
