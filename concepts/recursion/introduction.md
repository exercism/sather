# Recursion

A routine can call itself. That sounds like it would go round forever, but
it doesn't have to: each call is handed a **smaller** problem, and the
smallest problem of all is answered straight away.

This is called **recursion**, and a routine that calls itself is
**recursive**.

## Counting digits

How many digits does a number have? A number below ten has one. Any bigger
number has one more digit than the same number with its last digit knocked
off, and `/ 10` knocks off the last digit.

```sather
   digits(n : INT) : INT is
      if n < 10 then return 1 end;
      return 1 + digits(n / 10);
   end;
```

Here is what happens for `digits(472)`:

```
digits(472) = 1 + digits(47)
digits(47)  = 1 + digits(4)
digits(4)   = 1
```

`digits(4)` answers without calling anything. Then `digits(47)` can finish,
with `1 + 1`, and then `digits(472)` finishes with `1 + 2`, which is `3`.

Every recursive routine has these two parts:

- a **base case**: a problem so small that the answer is known. Here that is
  `n < 10`.
- a **recursive case**: the routine calls itself on a smaller problem, and
  uses that answer to build its own. Here that is `1 + digits(n / 10)`.

The base case comes first. If the routine called itself before checking,
it would never stop.

## Calling yourself more than once

A recursive case can make more than one call. A delivery rider is `east`
blocks west of the shop and `south` blocks north of it, and only ever rides
east or south. How many different routes are there?

If either distance is nought, the rider has to go in a straight line, so
there is only one route. Otherwise the first block is either east or south,
and the routes after each of those are a smaller problem:

```sather
   routes(east, south : INT) : INT is
      if east = 0 or south = 0 then return 1 end;
      return routes(east - 1, south) + routes(east, south - 1);
   end;
```

Both calls make the problem smaller, so both will reach the base case.

## Working along an array

An array does not get smaller, but the part still left to look at does. An
extra argument says where that part starts, and each call moves it one
place along. Does a name appear in a list, from position `from` onwards?

```sather
   appears(names : ARRAY{STR}, from : INT, wanted : STR) : BOOL is
      if from = names.size then return false end;
      return names[from] = wanted or appears(names, from + 1, wanted);
   end;
```

The base case is the empty part: once `from` has reached the end, there is
nothing left in which to find the name. To search the whole list, start at
`0`.

## `or` and `and` stop early

`or` doesn't look at its right-hand side if the left-hand side is already
true, because the answer is true whatever is on the right. In `appears`,
that means that once the name is found, no more calls are made.

`and` stops early in the same way when its left-hand side is false.

## When recursion goes wrong

If a call doesn't make the problem smaller, or a base case is missing, the
routine calls itself again and again. Each call that hasn't finished uses up
a little memory, and eventually there is none left and the program crashes.

When that happens, ask two questions:

- Is there a base case, and is it checked before the recursive call?
- Does every call get closer to that base case?
