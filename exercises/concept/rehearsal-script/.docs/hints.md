# Hints

## General

- Every task builds text in a loop, so every one starts with `#FSTR` and
  ends with `.str`.
- Assign the result of every `+` back into the builder:
  `script := script + ...`.

## 1. Repeat a cue

- `1.upto!(times)` runs the loop the right number of times. The value it
  gives is not needed, so it can go straight into a variable that is never
  used — or use `times.times!`, which gives nothing at all.
- No times at all needs no special handling: the loop simply does not run.

## 2. The cast initials

- `names.elt!` gives each name; `[0]` takes its first character.
- An `FSTR` accepts a `CHAR` directly, so there is no need to turn it into a
  string first.

## 3. Number the lines

- Two iterators in one loop, as in the last exercise: `1.up!` for the number
  and `lines.elt!` for the text.
- The new line goes *before* every line except the first. Testing the number
  is the easiest way: `if number > 1 then ... end`.
- An `FSTR` accepts the number directly, so `script + number + ". "` works
  without converting.

## 4. Shout a line

- `line.elt!` walks a string a character at a time.
- `.upper` leaves anything that is not a letter alone, so the space needs no
  special handling.
