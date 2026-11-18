# Math Functions

`FLTD` carries the usual mathematical functions as routines. Each is called
on the number it works on:

```sather
   x.sqrt          -- not sqrt(x)
   y.atan2(x)      -- not atan2(y, x)
```

## Constants

| Call | Value |
| --- | --- |
| `FLTD::pi` | π, 3.14159… |
| `FLTD::e` | *e*, 2.71828… |
| `FLTD::half_pi` | π / 2 |
| `FLTD::sqrt_2` | √2 |

The class name goes in front because a constant belongs to no particular
number.

## Roots and powers

| Routine | Answers |
| --- | --- |
| `x.sqrt` | the square root of `x` |
| `x.cube_root` | the cube root |
| `x.square` | `x * x` |
| `x.cube` | `x * x * x` |
| `x.pow(y)` | `x` to the power `y`, which need not be whole |

## Trigonometry

| Routine | Answers |
| --- | --- |
| `a.sin` `a.cos` `a.tan` | for an angle `a` in radians |
| `x.asin` `x.acos` `x.atan` | the angle, in radians, whose sine, cosine or tangent is `x` |
| `y.atan2(x)` | the angle, in radians, from the positive `x` direction to the point (`x`, `y`) |

Every angle is in **radians**: a whole turn is 2π, not 360. Convert at the
edges and work in radians in between:

```sather
   radians ::= degrees * FLTD::pi / 180.0d;
   degrees ::= radians * 180.0d / FLTD::pi;
```

`.atan2` is better than `.atan` for finding a direction. `(y / x).atan` cannot
tell (1, 1) from (−1, −1), since both divide to `1.0`, and fails when `x` is
zero. `y.atan2(x)` looks at both signs and answers anywhere from −π to π.

## Exponentials and logarithms

| Routine | Answers |
| --- | --- |
| `x.exp` | *e* to the power `x` |
| `x.log` | the natural logarithm: the power *e* must be raised to, to give `x` |
| `x.log10` | the logarithm base 10 |
| `x.log2` | the logarithm base 2 |
| `x.exp2` `x.exp10` | 2 or 10 to the power `x` |

`exp` and `log` undo each other, as do `exp10` and `log10`, and `exp2` and
`log2`. The introduction shows `exp10` and `log10` worked through for a run
of powers of ten.

Something that shrinks by the same fraction each step follows
`start * (-rate * t).exp`; the time it takes to fall from `start` to
`level` is `(start / level).log / rate`.

## When the answer does not exist

None of these raise an exception. A question with no real answer gives one of
the special `FLTD` values instead, which then spreads through any arithmetic
it touches:

```sather
   (-1.0d).sqrt         -- NaN, "not a number"; prints as -nan
   0.0d.log             -- -inf
   (-1.0d).log          -- NaN
```

`x.is_nan` and `x.is_inf` test for them. Check an argument before the call
when a bad one is possible; a `NaN` found three calculations later is hard to
trace back.

## Rounding is approximate here too

These routines answer the nearest `FLTD`, not the exact value, so the usual
rule applies: compare results with a tolerance, never with `=`.

```sather
   (FLTD::pi / 6.0d).sin      -- 0.5, or very nearly
```
