# Hints

## General

- Every routine here answers yes or no, so every one is declared `: BOOL`.
- None of them needs an `if`. The operators already produce the answer.

## 1. Is the mat ready?

- Both things have to be true, so `and`.

## 2. Is there something to land on?

- Either will do, so `or`.

## 3. Who still needs the briefing?

- The answer is the opposite of the argument. `~` flips it, and nothing
  else is needed.

## 4. Is this performer old enough?

- Thirteen counts as old enough, so the comparison is `>=` rather than `>`.
- Return the comparison itself. There is no need for `if`.

## 5. Put it all together

- Three things all have to hold, so two `and`s.
- You already wrote routines for two of them. Inside the same class you can
  call them by name, passing on the arguments each one needs, and join the
  answers they give.
