# Hints

## General

- The stub already declares the four attributes. Write the routines below
  them, inside the class.
- Inside the class an attribute is used by name, with no object in front:
  `home_score`, not `board.home_score`.

## 1. Set up the board

- `create` returns `SAME`, and starts with `board ::= new;`.
- Set the two team names from the arguments and return the object.
- The scores need no setting. An `INT` attribute starts at nought already.

## 2. Score a goal

- These answer nothing, so they are declared with no `:` and no type at all:
  `home_goal is`.
- The body is one line: add one to the score and put it back.

## 3. Read the board

- Four pieces joined with `+`, with the spaces inside the quotes.
- `+` will join a number onto a string, so the scores need no converting.

## 4. Who is winning?

- Three cases, and they are comparisons rather than fixed values, so this is
  an `if` chain and not a `case`.
- Check for the draw as one of the three, not as an afterthought.

## 5. How far ahead?

- Subtract one score from the other and use `.abs`, so the order does not
  matter.
