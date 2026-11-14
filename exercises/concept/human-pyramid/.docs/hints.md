# Hints

## General

- Each routine needs a base case, checked first, and a recursive case that
  calls the same routine on a smaller problem.
- Inside the class a routine can call itself by name, just as `digits` does
  in the introduction.

## 1. Count the acrobats

- The base case is the pyramid with no rows.
- A pyramid is its bottom row plus a pyramid with one row fewer.

## 2. Climb the rope ladder

- Think about the **last** step of the climb. It was either one rung or two.
- If the last step was one rung, how many rungs were climbed before it? And
  if it was two?
- One rung can only be climbed one way. So can nought rungs, which is
  "already there", and that is a convenient second base case.
- This makes two recursive calls, like `routes` in the introduction.

## 3. Balance the see-saw

- There are two base cases. When is the answer certainly yes, and when are
  there no acrobats left to try?
- For the acrobat at `from` there are two choices: they go on the see-saw,
  or they don't. Each choice leaves a smaller question about the acrobats
  after them.
- If they go on, the rest have less weight to make up.
- The answer is yes if either choice works. `or` tries the second choice
  only when the first one fails.
