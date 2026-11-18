# Hints

## General

- Every routine is called on the number it works on: `x.sqrt`, not `sqrt(x)`.
- `FLTD::pi` is π. Write the class name in front.

## 1. Rope for the boundary

- Three things multiplied together, one of them `FLTD::pi`.

## 2. How far from the pitch?

- Work out x² + y² first, in brackets, then call `.sqrt` on the bracket.

## 3. Which way did it go?

- `.atan2` is called on the across distance `y`, with the down-the-ground
  distance `x` as its argument.
- Its answer is in radians. Multiply by `180.0d` and divide by `FLTD::pi` to
  get degrees.

## 4. How far did it carry?

- `.sin` wants radians, and `angle` is in degrees. Convert it first, then
  double it.
- Converting is the reverse of task 3: multiply by `FLTD::pi` and divide by
  `180.0d`.

## 5. Slowing on the grass

- e to a power is `.exp`, called on the power: `(-0.02d * metres).exp`.

## 6. Where will it stop being worth chasing?

- ln is `.log`. Call it on the bracketed `speed / target`, then divide.
