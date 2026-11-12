# Hints

## General

- Every task builds text in a loop, so every one starts with `#FSTR` and
  ends with `.str`.
- Assign the result of every `+` back into the builder, every time.

## 1. Repeat a cue

- `upto!`, counting from one up to the number given, runs the loop the
  right number of times. The value it gives is not needed, so it can go
  straight into a variable that is never used — or use `times!` on the
  number, which gives nothing at all.
- No times at all needs no special handling: the loop simply does not run.

## 2. The cast initials

- `elt!` on the array gives each name; `[0]` on a string takes its first
  character.
- An `FSTR` accepts a `CHAR` directly, so there is no need to turn it into a
  string first.

## 3. Number the lines

- Two iterators in one loop, as in the last exercise: `up!` counting from
  one for the number, and `elt!` for the text.
- The new line goes *before* every line except the first. Testing the number
  is the easiest way to tell the first from the rest.
- An `FSTR` accepts the number directly, so there is no need to convert it
  before adding it.

## 4. Shout a line

- `elt!` on a string walks it a character at a time.
- `.upper` leaves anything that is not a letter alone, so the space needs no
  special handling.
