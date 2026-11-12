# Floating-point Numbers

`INT` holds whole numbers only, and dividing two of them throws away the
remainder:

```sather
7 / 4        -- 1, not 1.75
```

When the fraction matters, the type is `FLTD` — a **floating-point** number,
which can hold values between the whole ones.

## Writing one

A floating-point literal has a decimal point and a `d` at the end.

```sather
   water_temp : FLTD is
      return 24.5d;
   end;
```

The `d` is not optional. `24.5` on its own is a different type, of less
precision; the `d` asks for the one this track uses everywhere.

Write `3.0d`, not `3d` — there has to be a decimal point too.

## Arithmetic

`+`, `-`, `*` and `/` all work, and `/` now keeps the fraction:

```sather
7.0d / 4.0d      -- 1.75
```

Both sides have to be `FLTD`. Sather will not quietly mix the two types, so
`7 / 4.0d` is an error rather than a surprise.

## From a whole number

`.fltd` turns an `INT` into an `FLTD`:

```sather
   litres(cubic_cm : INT) : FLTD is
      return cubic_cm.fltd / 1000.0d;
   end;
```

A fish tank holding 1500 cubic centimetres holds `litres(1500)`, which is
`1.5`. Note where the conversion goes: `(1500 / 1000).fltd` would be `1.0`,
because the division would already have thrown the half away.
Convert **before** dividing, not after.

## How far apart?

`.abs` throws away a minus sign, which is how to ask how far apart two
values are without caring which is bigger:

```sather
(24.5d - 26.0d).abs      -- 1.5
```
