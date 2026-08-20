# Floating-point Numbers

`INT` holds whole numbers only, and dividing two of them throws away the
remainder:

```sather
7 / 2        -- 3, not 3.5
```

When the fraction matters, the type is `FLTD` — a **floating-point** number,
which can hold values between the whole ones.

## Writing one

A floating-point literal has a decimal point and a `d` at the end.

```sather
   concert_a : FLTD is
      return 440.0d;
   end;
```

The `d` is not optional. `440.0` on its own is a different type, of less
precision; the `d` asks for the one this track uses everywhere.

Write `2.0d`, not `2d` — there has to be a decimal point too.

## Arithmetic

`+`, `-`, `*` and `/` all work, and `/` now keeps the fraction:

```sather
7.0d / 2.0d      -- 3.5
```

Both sides have to be `FLTD`. Sather will not quietly mix the two types, so
`7 / 2.0d` is an error rather than a surprise.

## From a whole number

`.fltd` turns an `INT` into an `FLTD`:

```sather
   halve(n : INT) : FLTD is
      return n.fltd / 2.0d;
   end;
```

`halve(7)` is `3.5`. Note where the conversion goes: `(7 / 2).fltd` would
be `3.0`, because the division would already have thrown the half away.
Convert **before** dividing, not after.

## How far apart?

`.abs` throws away a minus sign, which is how to ask how far apart two
values are without caring which is bigger:

```sather
(440.0d - 442.0d).abs      -- 2.0
```
