# Hints

## General

- Every task here is one loop with no counter and no `until!`. The
  iterators end it.
- Ask each iterator exactly once per turn and put the value in a variable.
  Writing `first.elt!` twice takes two bars instead of one.

## 1. How many bars do they play together?

- Call both iterators, then add one to a counter. There is nothing else to
  do with the values.
- The loop already ends when the shorter part runs out, so no comparison of
  sizes is needed.

## 2. How many bars match?

- Take one bar from each into variables, then compare them with `=`.

## 3. Who is busier?

- The same shape as task 2 with `>` instead of `=`. Note the order: the
  first part having more.

## 4. Weight the bars

- There is only one array here, but two iterators.
- `1.up!` counts 1, 2, 3 … and never stops. Paired with `part.elt!`, the
  array decides when the loop ends and `up!` supplies the numbers.
- Multiply the two together and add to a running total.
