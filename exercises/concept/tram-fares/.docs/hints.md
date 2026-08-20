# Hints

## General

- Each task compares one value against a fixed list, which is what `case` is
  for.
- Every `case` needs an `else`, even where the arms above it look complete.
  Without one, a value that matches nothing stops the program.

## 1. The fare for a zone

- Three `when` arms and an `else`. The `else` covers every number that is
  not a zone.
- Zone 0 and an unknown zone both cost nothing, but they are different
  cases; writing them as separate arms says what is meant.

## 2. What kind of ticket?

- `'c'` and `'s'` give the same answer, so they share one arm:
  `when 'c', 's' then`.
- Single quotes: the argument is a `CHAR`, not a `STR`.

## 3. What kind of day?

- Two arms, one listing two days and one listing five.
- Strings compare with `=` the same way numbers do, so they work in a
  `case` unchanged.

## 4. The daily cap

- You already have a routine that turns a day into a kind of day. Call it,
  then `case` on the answer.
- Doing it that way means the list of days is written once. Repeating it
  here is the mistake this task is shaped to catch.
