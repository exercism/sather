# Hints

## General

- Every task builds text in a loop, so every one starts with `#FSTR` and
  ends with `.str`.
- Assign the result of every `+` back into the builder, every time.

## 1. Repeat a cue

- `times!` on the number runs the loop that many times. It gives nothing,
  so there is nothing to name: `count.times!;` is a statement on its own.
- Nought needs no special handling: `0.times!` ends the loop before the
  body runs.

## 2. The cast initials

- `elt!` on the array gives each name; `[0]` on a string takes its first
  character.
- An `FSTR` accepts a `CHAR` directly, so there is no need to turn it into a
  string first.

## 3. Number the lines

- Two iterators in one loop, as in Duet Practice: `up!` counting from
  one for the number, and `elt!` for the text.
- The new line goes *before* every line except the first. Testing the number
  is the easiest way to tell the first from the rest.
- An `FSTR` accepts the number directly, so there is no need to convert it
  before adding it.

## 4. Shout a line

- `elt!` on a string walks it a character at a time.
- `.upper` leaves anything that is not a letter alone, so the space needs no
  special handling.
