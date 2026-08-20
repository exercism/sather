# Floating-point Numbers

`FLTD` holds a number that may have a fraction. A literal needs a decimal
point and a `d`:

```sather
   440.0d
   0.5d
   -2.25d
```

`FLT` is the same idea with half the precision. This track uses `FLTD`
throughout; there is no reason to reach for `FLT` unless memory is tight.

## Arithmetic

| Operator | Meaning |
| --- | --- |
| `+` `-` `*` | as for `INT` |
| `/` | division, keeping the fraction |

There is no `%` for `FLTD`.

Both operands must be `FLTD`. Mixing an `INT` in is a compile error, not a
silent conversion — which is a feature: the one place this bites is exactly
the place people get it wrong.

## Converting

```sather
   7.fltd            -- 7.0, an INT made into an FLTD
   7.5d.int          -- 7, the fraction thrown away
   7.5d.round        -- 8, to the nearest whole number
   7.5d.floor        -- 7.0, down to a whole number
   7.5d.ceiling      -- 8.0, up to a whole number
```

Convert before dividing, never after: `n.fltd / 2.0d` keeps the half,
`(n / 2).fltd` has already lost it.

## Useful routines

```sather
   (-2.5d).abs       -- 2.5
   2.0d.sqrt         -- 1.41421
   (2.0d).max(3.0d)  -- 3.0
```

## Floating-point is approximate

An `FLTD` holds a very close approximation, not the exact value. Most
decimal fractions cannot be stored exactly, in the same way that a third
cannot be written exactly in decimal. So:

```sather
0.1d + 0.2d          -- very nearly 0.3, but not exactly
```

Two consequences worth remembering:

**Do not compare with `=`.** Two calculations that should give the same
answer often differ in the last few digits. Ask whether they are close
instead:

```sather
   (a - b).abs < 0.0001d
```

**Adding many small values loses accuracy.** Each addition rounds a little,
and the errors build up.

When values must be exact — money, in particular — count in whole units
with `INT` (cents rather than dollars) instead.

## Printing

`.str` shows about six significant digits, which is short of the precision
actually held:

```sather
   #OUT + (1.0d / 3.0d).str;      -- 0.333333
```
