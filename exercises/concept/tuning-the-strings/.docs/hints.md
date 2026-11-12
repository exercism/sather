# Hints

## General

- Every routine here answers with a fraction, so every one is declared
  `: FLTD`.
- Constants in the arithmetic need the same type: a whole number written
  as an `FLTD` still needs its `.0d`.

## 1. Up an octave

- Twice the frequency is a multiplication, with an `FLTD` constant.

## 2. Down an octave

- Half is a division. Unlike `/` on whole numbers, `/` on `FLTD` keeps the
  half.

## 3. Halfway between

- Add them and halve. Brackets matter: `/` is done before `+`, so without
  brackets round the sum only the second frequency is halved.

## 4. How far out?

- Subtract one from the other, then `.abs` to drop any minus sign.
- Brackets again: `.abs` has to apply to the whole subtraction, not only to
  the second number.

## 5. Sharing out practice

- The two arguments are `INT`, and the answer is `FLTD`, so something has to
  convert.
- Convert both with `.fltd` **before** dividing. Dividing first would throw
  the fraction away, and converting afterwards cannot get it back.
