# Hints

## General

- Every routine here answers with a fraction, so every one is declared
  `: FLTD`.
- Constants in the arithmetic need the same type: `2.0d`, not `2`.

## 1. Up an octave

- Multiply by `2.0d`.

## 2. Down an octave

- Divide by `2.0d`. Unlike `/` on whole numbers, this keeps the half.

## 3. Halfway between

- Add them and halve. Brackets matter: `low + high / 2.0d` halves only
  `high`.

## 4. How far out?

- Subtract one from the other, then `.abs` to drop any minus sign.
- Brackets again: `.abs` has to apply to the subtraction, so
  `(played - target).abs`.

## 5. Sharing out practice

- The two arguments are `INT`, and the answer is `FLTD`, so something has to
  convert.
- Convert both with `.fltd` **before** dividing. Dividing first would throw
  the fraction away, and converting afterwards cannot get it back.
