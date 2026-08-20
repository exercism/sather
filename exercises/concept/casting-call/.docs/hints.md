# Hints

## General

- Each of these picks one of three answers, so each is an `if` with one
  `elsif` and one `else`.
- Ask the most demanding question first. If `score >= 5` is asked before
  `score >= 8`, the second can never be reached.

## 1. The verdict

- Three bands, so two questions: eight or more, then five or more,
  then everything left over.

## 2. Which group?

- Working upwards is easiest: under 13 first, then under 16, then the rest.
- "From 13 to 15" and "under 16" describe the same performers, and the
  second is one comparison instead of two.

## 3. When to come back

- `=` compares two strings: `if group = "Juniors" then`.
- Spell the group names exactly as task 2 returns them, capital letter and
  all.

## 4. What to write on the sheet

- The first case needs two things at once, so join them with `and`:
  `if score >= 8 and sings then`.
- The second case is reached only when the first has already failed, so it
  does not need to ask about singing again.
