# Hints

## General

- A routine answering with a character is declared `: CHAR`. One answering
  with a number is `: INT`, and one answering yes or no is `: BOOL`.

## 1. Is it a letter?

- `.is_alpha` gives the answer directly. Return it; no `if` is needed.

## 2. Shout it

- `.upper` already leaves non-letters alone, so there is nothing to check
  for.

## 3. What number is it?

- `.int`.

## 4. The first character

- Square brackets, and the first position is `0`.

## 5. Turn the wheel

- Three steps: work out how far along the alphabet the letter is, move it,
  then turn the answer back into a letter.
- How far along: the difference between the letter's number and the number
  for `a`. For `a` itself that is 0.
- Coming back round is `%` by the number of letters in the alphabet, which
  keeps the answer from 0 up to one less than that, even after a negative
  turn.
- Back into a letter: undo the first step, then use `.char`.
- Get the number for `a` with `.int` rather than writing `97`. It says why
  the number is there.
