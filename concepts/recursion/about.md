# Recursion

```sather
   digits(n : INT) : INT is
      if n < 10 then return 1 end;        -- base case
      return 1 + digits(n / 10);          -- recursive case
   end;
```

A recursive routine is one that calls itself. It needs:

- one or more **base cases**, answered without a recursive call, and checked
  first;
- a **recursive case**, which calls the routine on a strictly smaller
  problem and builds its answer from the result.

If every call moves closer to a base case, the recursion ends. If one
doesn't, it doesn't end, and the program runs out of stack and crashes.

## Several calls

A recursive case can make several calls, as `routes(east - 1, south) +
routes(east, south - 1)` does. Each call starts its own chain of calls, so
the amount of work can grow very fast: `routes` with ten blocks each way
makes over a hundred thousand calls. Recursion that recomputes the same
small problems again and again is a sign that a loop, or remembering earlier
answers, would be faster.

## Recursing along an array

Rather than copying ever-smaller arrays, pass the position where the
remaining part starts:

```sather
   appears(names : ARRAY{STR}, from : INT, wanted : STR) : BOOL is
      if from = names.size then return false end;
      return names[from] = wanted or appears(names, from + 1, wanted);
   end;
```

`and` and `or` evaluate their right-hand side only when they need to, so a
recursive call on the right is skipped once the answer is settled.

## Try one choice, then another

Many puzzles are solved by making a choice, solving what is left, and
trying a different choice if that fails. Recursion fits this well. Each
call makes one choice and leaves the rest to a recursive call, and `or`
moves on to the next choice only when the first one fails. When the choices
depend on what has been used so far, the usual pattern is a loop over the
candidates: mark one as used, recurse, then unmark it before trying the
next. This is called **backtracking**.

## Recursion or a loop?

Anything written with recursion can be written with a loop, and the other
way round. Sather does not promise to turn a call at the end of a routine
into a jump, so very deep recursion (hundreds of thousands of calls) can run
out of stack where a loop would not. Use recursion when the problem has the
same shape inside it, as trees, nested lists and searches do. Use a loop
when you are just stepping along.
